# db_file_store 

## Original comes from https://github.com/Aagam41/db_file_storage

This version removes a if statement that doesnt allow file access and creates invalid requests. (storge.py/_open)

## Integration


### In settings.py

- Add db_file_storage to installed apps 
```
INSTALLED_APPS = [
  'db_file_storage'
]
```

- Add default data storage 
```
DEFAULT_FILE_STORAGE = 'db_file_storage.storage.DatabaseFileStorage'
```

- Add static settings 
``` 
STATIC_URL = 'static/'  
STATIC_ROOT = BASE_DIR / 'static'
STATICFILES_DIR = [
  BASE_DIR / 'static',
  BASE_DIR / 'static/icon',
] 
``` 

### In main app urls.py

- Add image view and download urls to urlpatterns[]
```
from db_file_storage.compat import url
from db_file_storage import views as db_views

urlpatterns[
  ....,
  url(r'^download/', db_views.get_file, {'add_attachment_headers': True},
    name='db_file_storage.download_file'),
  url(r'^get/', db_views.get_file, {'add_attachment_headers': False},
     name='db_file_storage.get_file')
]

```

- Add static url route to urlpatterns[] in main urls.py
```
urlpatterns[] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

