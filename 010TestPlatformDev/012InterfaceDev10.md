### jiraExt模型定义

    扩展平台实现的需求
        * 缓存jira部分项目数据，用于查询
        * 项目管理、用例管理、缺陷管理
        * 提供部分更新jira数据功能

    1、jiraExt——>models.py中模型定义代码修改如下
    
```python
from django.db import models


# Create your models here.
# 项目
class JiraProject(models.Model):
    id = models.CharField('项目ID', max_length=32, unique=True)
    key = models.CharField('项目关键字', max_length=32, primary_key=True, )
    name = models.CharField('项目名称', max_length=256)
    description = models.CharField('项目描述', max_length=1024, default='')
    lead = models.CharField('项目负责人', max_length=32)
    projectTypeKey = models.CharField('项目类型', max_length=32)
    version = models.CharField('项目版本', max_length=128, default='')
    archived = models.BooleanField('是否归档', default=False)

    def __str__(self):
        return self.name

    class Meta:
        verbose_name = 'jira项目表'


# 用例
class JiraCase(models.Model):
    id = models.CharField('用例ID', max_length=32, unique=True)
    key = models.CharField('用例关键字', max_length=32, primary_key=True, )
    summary = models.CharField('用例主题', max_length=1024)
    description = models.CharField('用例描述', max_length=10240, null=True)
    creator = models.CharField('创建者', max_length=32)
    created = models.DateTimeField('创建时间')
    updated = models.DateTimeField('更新时间')
    project = models.ForeignKey(JiraProject, on_delete=models.CASCADE)
    labels = models.CharField('标签', max_length=128, default='')

    def __str__(self):
        return self.summary

    class Meta:
        verbose_name = 'jira用例表'


# 缺陷bug
class JiraBug(models.Model):
    id = models.CharField('缺陷ID', max_length=32, unique=True)
    key = models.CharField('缺陷关键字', max_length=32, primary_key=True, )
    summary = models.CharField('缺陷主题', max_length=1024)
    description = models.CharField('缺陷描述', max_length=10240, null=True)
    reporter = models.CharField('提交者', max_length=32)
    created = models.DateTimeField('创建时间')
    updated = models.DateTimeField('更新时间')
    project = models.ForeignKey(JiraProject, on_delete=models.CASCADE)
    status = models.CharField('状态', max_length=32, default='')

    def __str__(self):
        return self.summary

    class Meta:
        verbose_name = 'jira缺陷表'
```

    2、执行数据迁移命令到数据库
    
        * python manage.py makemigrations
        * python manage.py migrate
        注意：如果迁移失败，可以是多次迁移造成之前的迁移文件未删除，数据库的迁移记录也未删除
        
    3、同步前端dist文件
    
    4、jiraExt——>新建conf.py文件定义jira的host、登录用户、登录密码
    
```python
# coding=utf-8
# @File     : conf.py
# @Time     : 2021/4/22 15:07
# @Author   : jingan
# @Email    : 3028480064@qq.com
# @Software : PyCharm

jira_host = 'http://devops.sqtest.online:8070/'
jira_user = 'liaojingan'
jira_psw = '123456'
```

    5、jiraExt——>新建jira.yml配置文件定义模型属性
    
```python
project:
  - id
  - key
  - name
  - description
  - lead
  - projectTypeKey
  - version
  - archived

case:
  - id
  - key
  - summary
  - description
  - creator
  - created
  - updated
  - project
  - labels

bug:
  - id
  - key
  - summary
  - description
  - reporter
  - created
  - updated
  - project
  - status
```

    6、jiraExt——>新建plugins.py文件封装获取jira数据功能函数
    
```python
# coding=utf-8
# @File     : plugins.py
# @Time     : 2021/4/22 15:06
# @Author   : jingan
# @Email    : 3028480064@qq.com
# @Software : PyCharm

# 封装获取jira数据功能
import yaml
from jira import JIRA
from .conf import jira_host, jira_psw, jira_user

# 登录jira，获取客户端对象
jira = JIRA(jira_host, auth=(jira_user, jira_psw))

def _read_yml(path):
    with open(path, encoding='utf-8') as f:
        return yaml.safe_load(f.read())

# 获取项目数据，转化成字典形式
def query_project():
    # 从jira服务器获取项目——当前用户有权限的项目
    projects = jira.projects()
    # 从配置文件读取项目属性
    pro_fields = _read_yml('jiraExt/jira.yml')['project']
    res = []
    for project in projects:
        # 通过project.key获取单个项目对象
        pro = jira.project(project.key)  # 有lead 和 description其他属性
        item = {}
        for field in pro_fields:
            # 反射获取对象属性
            item[field] = str(getattr(pro, field, ''))
            res.append(item)
    return res

# 获取用例数据
def query_case():
    cases = jira.search_issues('issuetype =测试用例')
    case_fields = _read_yml('jiraExt/jira.yml')['case']  # 从配置文件读取项目属性
    res = []
    for case in cases:
        item = {}
        for field in case_fields:
            if field in ['id', 'key']:
                item[field] = getattr(case, field)  # 直接取id 或者 key
            else:
                item[field] = str(getattr(case.fields, field, ''))  # 其他类型需要通过fields取值
        item['project_id'] = item.pop('project')  # 修改key
        res.append(item)
    return res

# 获取bug数据
def query_bug():
    bugs = jira.search_issues('issuetype = 缺陷')
    _conf = _read_yml('jiraExt/jira.yml')['bug']
    res = []
    for bug in bugs:
        item = {}
        for one in _conf:
            if one in ['id', 'key']:
                item[one] = str(getattr(bug, one, ''))  # 直接转字符串
            else:
                item[one] = str(getattr(bug.fields, one, ''))
        res.append(item)
    return res
```    

    7、jiraExt——>views.py文件定义同步jira数据到本地函数以及本地查询jira数据的函数
    
```python
from django.core.paginator import Paginator
from django.http import JsonResponse
from django.shortcuts import render
from jiraExt.plugins import query_project, query_case, query_bug
from .models import JiraProject, JiraBug, JiraCase
from django.views.decorators.http import require_GET


# 同步jira项目数据
@require_GET
def sync_project(request):

    # 从Jira服务器获取jira中的项目数据，同步到本地
    retlist = query_project()
    # 将数据保存到本地数据库
    for ret in retlist:
        JiraProject.objects.update_or_create(**ret)  # 更新或创建
        # obj = JiraProject(**ret)
        # obj.save()  # 提交到数据库
    # 批量创建--大量数据会提高数据库利用率
    # pros = [JiraProject(**ret) for ret in retlist]
    # JiraProject.objects.bulk_update(pros,fields=['description','lead'])
    return JsonResponse({'retcode': 200, 'msg': '同步项目数据成功'})

# 从本地查询jira项目数据
@require_GET
def list_project(request):
    in_params = request.GET
    info = {}  # 入参过滤器
    if '_id' in in_params:
        info['id'] = in_params.get['_id']

    # 获取分页数据--page_size,page_index
    page_size = in_params.get('page_size', 5)  # 默认1页显示5条
    page_index = in_params.get('page_index', 1)  # 默认第一页
    # 初始化分页器
    paginator = Paginator(list(JiraProject.objects.filter(**info).values()), page_size)
    # 根据页码提供当前页内容
    retlist = list(paginator.get_page(page_index))
    return JsonResponse({'retcode': 200, 'retlist': retlist, 'total': paginator.count})

# 同步用例
def sync_case(request):
    retlist = query_case()
    # 数据保存到本地数据库
    for ret in retlist:
        JiraCase.objects.update_or_create(**ret)  # 更新或创建
    return JsonResponse({'retcode': 200, 'msg': '同步用例数据成功'})

@require_GET
def list_case(request):
    in_params = request.GET
    info = {}  # 入参过滤容器
    if '_id' in in_params:
        info['id'] = in_params.get('_id')

    # 获取分页数据--page_size,page_index
    page_size = in_params.get('page_size', 5)  # 默认1页显示5条
    page_index = in_params.get('page_index', 1)  # 默认第一页
    # 初始化分页器
    paginator = Paginator(list(JiraCase.objects.filter(**info).values()), page_size)
    # 根据页码提供当前页内容
    retlist = list(paginator.get_page(page_index))
    return JsonResponse({'retcode': 200, 'retlist': retlist, 'total': paginator.count})

def sync_bug(request):
    retlist = query_bug()
    for res in retlist:
        res['project_id'] = res.pop('project')
        JiraBug.objects.update_or_create(**res)
    return JsonResponse({'retcode': 200, 'msg': '同步成功'})

def list_bug(request):
    in_params = request.GET
    info = {}
    if '_id' in in_params:
        info['id'] = in_params.get('_id')

    # 获取分页数据--page_size,page_index
    page_size = in_params.get('page_size', 5)  # 默认1页显示5条
    page_index = in_params.get('page_index', 1)  # 默认第一页
    # 初始化分页器
    paginator = Paginator(list(JiraBug.objects.filter(**info).values()), page_size)
    # 根据页码提供当前页内容
    retlist = list(paginator.get_page(page_index))
    return JsonResponse({'retcode': 200, 'retlist': retlist, 'total': paginator.count})
```
    8、autotpsite——>urls.py设置主路由
    
```python
from sqtp import urls
from django.contrib import admin
from django.urls import path, include
from django.conf.urls.static import static
from jiraExt import urls as jira_url

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include(urls)),
    # 假设访问地址不是以api开头的，就会选择到static静态文件路径中，静态文件的根目录是dist
    # 如果前端访问了projects路径就会对应动态渲染前端的projects.html文件
    path('jira/',include(jira_url)),
]+static("/", document_root="dist")
```

    9、jiraExt——>新建urls.py文件设置路由
    
```python
# coding=utf-8
# @File     : urls.py
# @Time     : 2021/4/22 15:37
# @Author   : jingan
# @Email    : 3028480064@qq.com
# @Software : PyCharm

from django.urls import path, include
from .views import sync_project, list_project, sync_case, list_case, sync_bug, list_bug


urlpatterns = [
    path('sync/project/', sync_project),
    path('list/project/', list_project),
    path('sync/case/', sync_case),
    path('list/case/', list_case),
    path('sync/bug/', sync_bug),
    path('list/bug/', list_bug),
]
```
    
        