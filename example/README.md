# Example project for django-tagulous

This example project is configured for Django 3.2; Python 3.9 recommended.

You can see a static demo version of this example app at
https://radiac.net/projects/django-tagulous/demo/

To set it up and run the live version in a self-contained virtualenv::

    python -m venv .venv
    source .venv/bin/activate
    cd tagulous-example
    pip install "Django~=3.2"
    pip install -e git+https://github.com/radiac/django-tagulous.git#egg=django-tagulous
    cd src/django-tagulous/example
    export PYTHONPATH=..
    python manage.py migrate
    python manage.py createsuperuser
    python manage.py initial_tags
    python manage.py runserver

You can then visit the example site at http://localhost:8000/
