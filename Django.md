# Celery

## 配置

1. `pip install celery==4.4.2`

2. 在项目根应用下创建`celery.py`

   ```python
   import os
   from celery import Celery
   
   # set the default Django settings module for the 'celery' program.
   os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'Anki.settings')
   
   app = Celery('Anki')
   
   app.config_from_object('django.conf:settings', namespace='CELERY')
   app.autodiscover_tasks()
   ```

   > Celery will look for a tasks.py file in each application directory of applications added to INSTALLED_APPS in order to load asynchronous tasks defined in it.

3. 在同一文件夹下的`__init__.py`，保证Django启动时Celery也启动：

   ```python
   # import celery
   from .celery import app as celery_app
   
   __all__ = ['celery_app']
   ```

   

