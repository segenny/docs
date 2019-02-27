# [API STORE][docs]

### Waple Platform
당신의 API Business를 효율적으로 관리해 줄 OPEN API 플랫폼 “Waple”

### API STORE 주요기능
API 스토어는 API 관리를 위한 자체 개발 솔루션 ‘Waple’을 통해 안정적인 서비스를 제공하고 있습니다. 
다수의 고객사가 다수의 API를 등록, 발급하는 과정에서 발생하는 여러가지 이슈들을 통합적으로 고려하여 Waple Platform에서 기업들이 API를 안정적으로 유지, 관리할 수 있습니다.

API 스토어는 개발자 지원사항을 포함한 API 서비스 센터와 API 관리를 위한 API 관리 센터로 구성됩니다. 고객사는 API 스토어 서비스 센터를 이용하여 API를 등록 또는 구매할 수 있습니다.

Waple Admin(제어정보관리 및 통계생성), Service(API호출처리 및 호출제어), DB(데이터 저장), Cache(분산 캐싱), Adapter(가상 API) 총 5개의 서버 시스템으로 구성되어 있습니다.

### API 스토어 시스템 구성도
**API 스토어를 통해 등록된 API는 다음과 같은 형태로 서비스를 제공하고 있습니다.**
![Image of Yaktocat](//www.apistore.co.kr/images/renew/bi_apistore.png)
<img src="https://www.apistore.co.kr/images/renew_2017/vi_waple_01.gif">


![2222222222222Image of Yaktocat](https://www.apistore.co.kr/images/renew/bi_apistore.png)

# a

[![][rover-img]][rover-url]
[![][sentry-img]][sentry-url]
[![][stream-img]][stream-url]
[![][rollbar-img]][rollbar-url]
[![][cadre-img]][cadre-url]
[![][load-impact-img]][load-impact-url]
[![][kloudless-img]][kloudless-url]
[![][auklet-img]][auklet-url]
[![][lightson-img]][lightson-url]

Many thanks to all our [wonderful sponsors][sponsors], and in particular to our premium backers, [Rover][rover-url], [Sentry][sentry-url], [Stream][stream-url], [Rollbar][rollbar-url], [Cadre][cadre-url], [Load Impact][load-impact-url], [Kloudless][kloudless-url], [Auklet][auklet-url], and [Lights On Software][lightson-url].

---

# Overview

Django REST framework is a powerful and flexible toolkit for building Web APIs.

Some reasons you might want to use REST framework:

* The [Web browsable API][sandbox] is a huge usability win for your developers.
* [Authentication policies][authentication] including optional packages for [OAuth1a][oauth1-section] and [OAuth2][oauth2-section].
* [Serialization][serializers] that supports both [ORM][modelserializer-section] and [non-ORM][serializer-section] data sources.
* Customizable all the way down - just use [regular function-based views][functionview-section] if you don't need the [more][generic-views] [powerful][viewsets] [features][routers].
* [Extensive documentation][docs], and [great community support][group].

There is a live example API for testing purposes, [available here][sandbox].

**Below**: *Screenshot from the browsable API*

![Screenshot][image]

----

# Requirements

* Python (2.7, 3.4, 3.5, 3.6, 3.7)
* Django (1.11, 2.0, 2.1, 2.2)

We **highly recommend** and only officially support the latest patch release of
each Python and Django series.

# Installation

Install using `pip`...

    pip install djangorestframework

Add `'rest_framework'` to your `INSTALLED_APPS` setting.

    INSTALLED_APPS = (
        ...
        'rest_framework',
    )

# Example

Let's take a look at a quick example of using REST framework to build a simple model-backed API for accessing users and groups.

Startup up a new project like so...

    pip install django
    pip install djangorestframework
    django-admin startproject example .
    ./manage.py migrate
    ./manage.py createsuperuser


Now edit the `example/urls.py` module in your project:

```python
from django.conf.urls import url, include
from django.contrib.auth.models import User
from rest_framework import serializers, viewsets, routers

# Serializers define the API representation.
class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ('url', 'username', 'email', 'is_staff')


# ViewSets define the view behavior.
class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer


# Routers provide a way of automatically determining the URL conf.
router = routers.DefaultRouter()
router.register(r'users', UserViewSet)


# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    url(r'^', include(router.urls)),
    url(r'^api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```

We'd also like to configure a couple of settings for our API.

Add the following to your `settings.py` module:

```python
INSTALLED_APPS = (
    ...  # Make sure to include the default installed apps here.
    'rest_framework',
)

REST_FRAMEWORK = {
    # Use Django's standard `django.contrib.auth` permissions,
    # or allow read-only access for unauthenticated users.
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'
    ]
}
```

That's it, we're done!

    ./manage.py runserver

You can now open the API in your browser at `http://127.0.0.1:8000/`, and view your new 'users' API. If you use the `Login` control in the top right corner you'll also be able to add, create and delete users from the system.

You can also interact with the API using command line tools such as [`curl`](https://curl.haxx.se/). For example, to list the users endpoint:

    $ curl -H 'Accept: application/json; indent=4' -u admin:password http://127.0.0.1:8000/users/
    [
        {
            "url": "http://127.0.0.1:8000/users/1/",
            "username": "admin",
            "email": "admin@example.com",
            "is_staff": true,
        }
    ]

Or to create a new user:

    $ curl -X POST -d username=new -d email=new@example.com -d is_staff=false -H 'Accept: application/json; indent=4' -u admin:password http://127.0.0.1:8000/users/
    {
        "url": "http://127.0.0.1:8000/users/2/",
        "username": "new",
        "email": "new@example.com",
        "is_staff": false,
    }

# Documentation & Support

Full documentation for the project is available at [https://www.django-rest-framework.org/][docs].

For questions and support, use the [REST framework discussion group][group], or `#restframework` on freenode IRC.

You may also want to [follow the author on Twitter][twitter].

# Security

If you believe you've found something in Django REST framework which has security implications, please **do not raise the issue in a public forum**.

Send a description of the issue via email to [rest-framework-security@googlegroups.com][security-mail].  The project maintainers will then work with you to resolve any issues where required, prior to any public disclosure.

[build-status-image]: https://secure.travis-ci.org/encode/django-rest-framework.svg?branch=master
[travis]: https://travis-ci.org/encode/django-rest-framework?branch=master
[coverage-status-image]: https://img.shields.io/codecov/c/github/encode/django-rest-framework/master.svg
[codecov]: https://codecov.io/github/encode/django-rest-framework?branch=master
[pypi-version]: https://img.shields.io/pypi/v/djangorestframework.svg
[pypi]: https://pypi.org/project/djangorestframework/
[twitter]: https://twitter.com/_tomchristie
[group]: https://groups.google.com/forum/?fromgroups#!forum/django-rest-framework
[sandbox]: https://restframework.herokuapp.com/

[funding]: https://fund.django-rest-framework.org/topics/funding/
[sponsors]: https://fund.django-rest-framework.org/topics/funding/#our-sponsors

[rover-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/rover-readme.png
[sentry-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/sentry-readme.png
[stream-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/stream-readme.png
[rollbar-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/rollbar-readme.png
[cadre-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/cadre-readme.png
[load-impact-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/load-impact-readme.png
[kloudless-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/kloudless-readme.png
[auklet-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/auklet-readme.png
[lightson-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/lightson-readme.png

[rover-url]: http://jobs.rover.com/
[sentry-url]: https://getsentry.com/welcome/
[stream-url]: https://getstream.io/try-the-api/?utm_source=drf&utm_medium=banner&utm_campaign=drf
[rollbar-url]: https://rollbar.com/
[cadre-url]: https://cadre.com/
[load-impact-url]: https://loadimpact.com/?utm_campaign=Sponsorship%20links&utm_source=drf&utm_medium=drf
[kloudless-url]: https://hubs.ly/H0f30Lf0
[auklet-url]: https://auklet.io/
[lightson-url]: https://lightsonsoftware.com

[oauth1-section]: https://www.django-rest-framework.org/api-guide/authentication/#django-rest-framework-oauth
[oauth2-section]: https://www.django-rest-framework.org/api-guide/authentication/#django-oauth-toolkit
[serializer-section]: https://www.django-rest-framework.org/api-guide/serializers/#serializers
[modelserializer-section]: https://www.django-rest-framework.org/api-guide/serializers/#modelserializer
[functionview-section]: https://www.django-rest-framework.org/api-guide/views/#function-based-views
[generic-views]: https://www.django-rest-framework.org/api-guide/generic-views/
[viewsets]: https://www.django-rest-framework.org/api-guide/viewsets/
[routers]: https://www.django-rest-framework.org/api-guide/routers/
[serializers]: https://www.django-rest-framework.org/api-guide/serializers/
[authentication]: https://www.django-rest-framework.org/api-guide/authentication/
[image]: https://www.django-rest-framework.org/img/quickstart.png

[docs]: https://www.django-rest-framework.org/
[security-mail]: mailto:rest-framework-security@googlegroups.com
