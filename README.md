Docker commands:

$ cd python-docker
$ pip install Flask

To create project specific requirement.txt file..use below pipreqs command.

$ pip install pipreqs
$ pipreqs

For overall system requirement.
$ pip freeze > requirements.txt
$ touch app.py

Open app.py and write below code.

from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!’

navigate to the working directory you created and run below command
$ python -m flask run

To test that the application is working properly, open a new browser and navigate to http://localhost:5000.

Create a Dockerfile for Python
Dockerfile
# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

CMD [ "python3", "-m" , "flask", "run", “--host=0.0.0.0"]

Directory structure - Make sure project structure is as below

python-docker
|____ app.py
|____ requirements.txt
|____ Dockerfile

docker build command creates image
$ docker build --tag python-docker .

View local images
$ docker images

Run your image as a container
$ docker run python-docker
$ docker run --publish 5000:5000 python-docker

$ curl localhost:5000
Hello, Docker!

Well Done!

List containers
$ docker ps

Stop container

$ docker stop wonderful_kalam
Restart containers

$ docker restart wonderful_kalam

To remove containers-
$ docker rm wonderful_kalam agitated_moser goofy_khayyam

To name a container, we just need to pass the --name flag to the docker run command.
$ docker run -d -p 5000:5000 --name rest-server python-docker
