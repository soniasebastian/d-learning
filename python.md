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


   commands used
       1  sudo apt update -y
    2  sudo apt install docker.io -y
    3  history
    4  sudo systemctl status docker
    5  clear
    6  docker run hello-world
    7  sudo usermod -aG docker ubuntu
    8  docker run hello-world
    9  logout
   10  docker run hello-world
   11  source 
   12  clear
   13  sudo systemctl status docker
   14  clear
   15  git clone https://github.com/soniasebastian/docker-learning.git
   16  cd docker-learning/
   17  ls
   18  cd exampl
   19  cd examples
   20  ls
   21  cat app.py
   22  cd first-docker-file/
   23  ls
   24  cat app.py
   25  vim Docker
   26  cd docker-learning/
   27  cd examples
   28  cd first-docker-file/
   29  ls
   30  vim Dockerfile
   31  history
   32  clear
   33  docker build -t soniasebastian/my-first-docker-image:latest .
   34  docker build -t soniasebastian011/my-first-docker-image:latest .
   35  docker build -t abhishekf5/my-first-docker-image:latest .
   36  ls
   37  cd docker-learning/
   38  cd examples
   39  cd first-docker-file/
   40  ls
   41  docker build -t soniasebastian/my-first-docker-image:latest .
   42  docker run -it soniasebastian/my-first-docker-image:latest .
   43  docker run -it soniasebastian/my-first-docker-image:latest
   44  clear
   45  docker login
   46  docker images
   47  docker push soniasebastian/my-first-docker-image:latest
   48  docker pull soniasebastian/my-first-docker-image:latest
   49  docker images
   50  cd docker-learning/
   51  cd examples/
   52  cd python-web-app/
   53  clear
   54  ls
   55  snap
   56  ls
   57  docker build .
   58  docker images
   59  docker run -it cdee3bfaf258
   60  docker run -p 8000 -it cdee3bfaf258
   61  docker run -p 8000:8000 -it cdee3bfaf258
   62  python manage.py migrate
   63  python3 manage.py migrate
   64  docker run -p 8000:8000 -it cdee3bfaf258
   65  history

   Also go to EC-2 instance and to seurity edit inbound rules
   add TCP PORT TO 8000
   THEN USE URL
        http://54.226.37.18:8000/demo/

   










         


