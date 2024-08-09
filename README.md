# Django Tagulous - Fabulous Tags


[![PyPI](https://img.shields.io/pypi/v/django-tagulous.svg)](https://pypi.org/project/django-tagulous/)
[![Documentation](https://readthedocs.org/projects/django-tagulous/badge/?version=latest)](https://django-tagulous.readthedocs.io/en/latest/)
[![Tests](https://github.com/radiac/django-tagulous/actions/workflows/ci.yml/badge.svg)](https://github.com/radiac/django-tagulous/actions/workflows/ci.yml)
[![Coverage](https://codecov.io/gh/radiac/django-tagulous/branch/main/graph/badge.svg?token=BCNM45T6GI)](https://codecov.io/gh/radiac/django-tagulous)

A tagging library for Django built on ForeignKey and ManyToManyField, giving
you all their normal power with a sprinkling of tagging syntactic sugar.

* [Project site](https://radiac.net/projects/django-tagulous/)
* [Source code](https://github.com/radiac/django-tagulous)
* [Documentation](https://django-tagulous.readthedocs.io/)
* [Changelog](https://django-tagulous.readthedocs.io/en/latest/changelog.html)


## Features

* Easy to install - simple requirements, **simple syntax**, lots of options
* Based on ForeignKey and ManyToManyField, so it's **easy to query**
* **Autocomplete** support built in, if you want it
* Supports multiple independent tag fields on a single model
* Can be used as a user-customisable CharField with choices
* Supports **trees of nested tags**, for detailed categorisation
* Admin support for managing tags and tagged models

Supports Django 2.2+, on Python 3.6+.


See the [Documentation](https://django-tagulous.readthedocs.io/)
for details of how Tagulous works; in particular:

* [Installation](https://django-tagulous.readthedocs.io/en/latest/installation.html) -
  how to install Tagulous
* [Example Usage](https://django-tagulous.readthedocs.io/en/latest/usage.html) -
  see examples of Tagulous in use
* [Upgrading](https://django-tagulous.readthedocs.io/en/latest/upgrading.html) -
  how to upgrade Tagulous, and see what has changed in the
  [changelog](https://django-tagulous.readthedocs.io/en/latest/changelog.html)
* [Contributing](https://django-tagulous.readthedocs.io/en/latest/contributing.html) -
  for how to contribute to Tagulous


Quickstart
==========

Install with `pip install django-tagulous`, add `tagulous` to Django's `INSTALLED_APPS`
and
[define the serializers](http://radiac.net/projects/django-tagulous/documentation/installation/),
then start adding tag fields to your model:

```python
from django.db import models
from tagulous.models import SingleTagField, TagField

class Person(models.Model):
    name = models.CharField(max_length=255)
    title = SingleTagField(initial="Mr, Mrs, Miss, Ms")
    skills = TagField()
```

You can now set and get them using strings, lists or querysets::

```python
myperson = Person.objects.create(name='Bob', title='Mr', skills='run, hop')
# myperson.skills == 'run, hop'
myperson.skills = ['jump', 'kung fu']
myperson.save()
# myperson.skills == 'jump, "kung fu"'
runners = Person.objects.filter(skills='run')
```

Behind the scenes your tags are stored in separate models (by default), so
because the fields are based on ``ForeignKey`` and ``ManyToManyField`` more
complex queries are simple::

```python
qs = MyRelatedModel.objects.filter(
    person__skills__name__in=['run', 'jump'],
)
```

As well as this you also get autocompletion in public and admin forms,
automatic slug generation, unicode support, you can build tag clouds easily,
and can nest tags for more complex categorisation.
