# Week 1 — App Containerization

## Containeraized backend
#image
cd backend-flask

export FRONTEND_URL="*"

export BACKEND_URL="*"

python3 -m flask run --host=0.0.0.0 --port=4567

cd ..

## Added docker file in backend flask

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
#. means every thing the current directory
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

## build container

docker build -t  backend-flask ./backend-flask
# open the port
# add shell to docker 

## Run container using this command
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask


## list the container images
docker images

# # contenarized frond-end
# cd to the front end directory.
installed npm using npm i command
there also created docker file
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]

# build container using this command
 # docker build -t frontend-react-js ./frontend-react-js
# after created the decompose file file in the root folder using docker-compose.yml using th exact name otherwise it will give error
# docker-compose.yml
#version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./frontend-react-js
    ports:
      - "3000:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js







