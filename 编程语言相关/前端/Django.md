# 初始化
## 安装
```shell
pip install django
```
## 创建项目
1.新建一个web框架工程，名为`mysite`
```shell
django-admin startproject mysite
```
2.1.创建一个具体应用
```shell
python manage.py startapp helloapp
```
2.2.修改这个应用的`view.py`
在`view.py`中实现业务
```python
from django.http import HttpResponse

def hello(request):
	return HttpResponse("Hello World! I am coming...")
```
2.3.修改主应用`mysite`下的`urls.py`文件，为具体应用创建路由
```python
# ...
from helloapp import views

urlpatterns=[
	 path('index/',views.hello),
	 # ...
]
```
## 运行
```shell
python manage.py runserver
```
