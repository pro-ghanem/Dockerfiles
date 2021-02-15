#A web server faces the outside world. It can serve files (HTML, images, CSS, etc) directly from the file system. However, it can’t talk directly to Django applications; it needs something that will run the application, feed it requests from web clients (such as browsers) and return responses.
A Web Server Gateway Interface - WSGI - does this job. WSGI is a Python standard.
uWSGI is a WSGI implementation. 


#here is how is things work in the background
the web client <-> the web server <-> uwsgi <-> Django


################################ AT THE BOTTOM LINE ####################################33
we need :
webserver >> send requests to >> the code/framework
so we need intermediator 

web server  <-> wsgi <-> code/framework
nginx   <-> uwsgi/gunicorn <-> django/flask

such as :  nginx  <-> fpm <-> php



here is the best way to understand there is a one in my github or python folder












#Django: Difference between using server through manage.py and other servers like gunicorn etc. Which is better?
python manage.py runserver 0.0.0.0:8000   and gunicorn hello_django.wsgi:application --bind 0.0.0.0:8000
```
- Django's built-in development web server (what you get when you run manage.py runserver) provides that functionality also, but it targets a development environment (e.g., restart when the code changes), whereas Gunicorn targets production.

Gunicorn has many features that Django's built-in server is lacking:

gunicorn can spawn multiple worker processes to parallelize incoming requests to multiple CPU cores
gunicorn has better logging
gunicorn is generally optimized for speed
gunicorn can be configured to fine grades depending on your setup
gunicorn is actively designed and maintained with security in mind

- manage.py runserver is only a development server, it is not meant for production under any circumstance.

```


# how to dockerize python code
https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/
