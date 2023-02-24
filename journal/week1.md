# Week 1 — App Containerization

##Containeraized backend
#image
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..

##Added docker file in backend flask
Create a file here: backend-flask/Dockerfile

FROM python:3.10-slim-buster
#inside the container
WORKDIR /backend-flask
#Outside the container—>Inside the container
#this contains the libraries want to install to run the app
COPY requirements.txt requirements.txt
#inside the container
#install the python libraries used for the app
RUN pip3 install -r requirements.txt
#outside container—>Inside the container
# . means every thing the current directory
#first period ./backend-flask(outside the container
#sedcond period ./backend-flask (inside the container)
COPY . .
#environment variable set it for environment in this case development
#set environment variables(Environment variables)
#inside the containers and will remains set when the container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}
#command
#this is the command to run the flaskpython3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]

