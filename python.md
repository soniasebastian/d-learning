           Python

Django application/requirements/communication b'w apps/containerize application
devops/dockerfile/requirements
dockerfile...>.devops(config...settings.py).demo..(application/one microservice)..python code(views.py..executed rendering templates folder)
demo_site.html url getting served on browser

        Flow of Django application

1.Django documentation
a. Install Django
b. Install python
c. import django to verify/pip install django etc....
d. django-admin startproject mysite
e. django is similar to ansible galaxy....skeleton of ansible role
f. django admin builds skeleton
g. django-admin startproject devops


created a project/nothing related to prj/ but only pjt configuration


        settings.py (settings python file for django project)
secret keys/ip whiteliste/template/web server gateways/db to connect/secure infor/django middlewares

              urls.py (serving the content)
    /demo is the context route which is serving content

           To create application
$python manage.py startapp demo
create applications

               views.py
actual code/index function /rendering an html file/placed in a template/content gets served


from dockerfile........>

ubuntu base image

workdir.../app....
for conatainerization........>requirements.text..python dependencies (django and tzdata)
devops/app...source code itself

both forms bundle/binary of application


execution fails as its ubuntu

we need python to install

RUN apt-get update.....python3 python-3-pip..pip install

      ENTRYPOINT and CMD in dcker container difference
execute as a start comand

     ENTRYPOINT ["python3"]
   CMD["manage.py", "runserver", "0.0.0.0:8000"]


   entrypoint cant be changed.....main executable in entrypoint..(cant change to node.js) ...non-overridable values
   http server remain same...parameters passing changes...passs more valuess...congigurable field that is CMD

   IF 8000 IS OCCUPIED....CAN BE CHANGED CMD

   










         


