Django Auth0 Auth
=================

*Django Auth0 Auth* allows you to authenticate through Auth0 in Django 2

Installation
------------

Run `pip install django2-auth0-auth`

Add the `Auth0Backend` to your `AUTHENTICATION_BACKENDS` setting:

```python
AUTHENTICATION_BACKENDS = (
    ...
    'auth0_auth.backends.Auth0Backend',
)
```

Add the `Auth0Middleware` to your `MIDDLEWARE` setting:


```python
MIDDLEWARE = [
    ...
    'auth0_auth.middleware.Auth0Middleware'
]
```

Edit your `urls.py` to include:

```python
from django.views.generic import RedirectView
```

```python
urlpatterns = [
    ...
    #Add this BEFORE you include the admin urls, so admin login will redirect to auth0 login
    path('admin/login/', RedirectView.as_view(pattern_name='auth0_login', permanent=False, query_string=True)),
    #Add the auth0 urls
    path('auth0/', include('auth0_auth.urls')),
    ...
]
```


Settings
--------

### AUTH0_DOMAIN

Auth0 domain.

### AUTH0_CLIENT_ID

Auth0 client id.


### AUTH0_CLIENT_SECRET

Auth0 client secret.


### AUTH0_SECRET_BASE64_ENCODED

**default:** `False`
Flag if Auth0 client secret is base64 encoded.


### AUTH0_SCOPE

**default:** `'openid email'`
OAuth scope parameter.


### AUTH0_RESPONSE_TYPE

**default:** `'code'`
OAuth response type parameter.


### AUTH0_USER_CREATION

**default:** `True`
Allow creation of new users after successful authentication.

Logging
-------
To enable logging add `auth0_auth` to `LOGGING['loggers']` options.

```python
LOGGING = {
    ...,
    'loggers': {
        ...,
        'auth0_auth': {
            'handlers': ['console'],
            'level': 'DEBUG',
        }
    }
}
```

