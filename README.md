tasks 20 

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY FILE 

CMD ["python", "app.py"]


from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello from Flask!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)


apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: flask-app
  template:
    metadata:
      labels:
        app: flask-app
    spec:
      containers:
      - name: flask-app
        image: your_docker_hub_username/flask-app:latest
        ports:
        - containerPort: 8080


apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: flask-app
  template:
    metadata:
      labels:
        app: flask-app
    spec:
      containers:
      - name: flask-app
        image: your_docker_hub_username/flask-app:latest
        ports:
        - containerPort: 8080



# Построить образ Docker
docker build -t your_docker_hub_username/flask-app:latest .

# Отправить образ в Docker Hub
docker push your_docker_hub_username/flask-app:latest

# Развернуть приложение в Kubernetes
kubectl apply -f deployment.yaml

tasks 21 

FROM nginx:latest

COPY index.html /usr/share/nginx/html/

<!DOCTYPE html>
<html>
<head>
  <title>Hello Docker</title>
</head>
<body>
  <h1>Hello, Docker!</h1>
</body>
</html>


docker build -t nginx-hello .
docker run -d -p 80:80 nginx-hello

tasks 22

const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.json({ message: 'Hello from Node.js!' });
});

app.listen(port, () => {
  console.log(Server running on port ${port});
});

FROM node:16

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY FILE 

CMD ["npm", "start"]

docker build -t node-hello .
docker run -d -p 3000:3000 node-hello
tasks 23

FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD mypassword
ENV MYSQL_DATABASE mydatabase
ENV MYSQL_USER myuser
ENV MYSQL_PASSWORD mypassword


docker build -t mysql-db .
docker run -d -p 3306:3306 --name mysql-db mysql-db

tasks 24

FROM python:3.9-slim AS build

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY FILE 

FROM python:3.9-slim

WORKDIR /app

COPY --from=build /app .

CMD ["python", "app.py"]

import pandas as pd

print("Hello from Pandas!")

docker build -t python-pandas .
docker run -it python-pandas

tasks 25

version: '3.7'

services:
  web:
    build: .
    ports:
      - "80:80"
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: mypassword
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: myuser
      MYSQL_PASSWORD: mypassword
    ports:
      - "3306:3306"

docker-compose up -d

tasks 26

FROM node:16-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY FILE 

CMD ["npm", "start"]

trigger:
  - master

pool:
  vmImage: 'ubuntu-latest'

variables:
  DOCKER_HUB_USERNAME: 'your_docker_hub_username'
  DOCKER_HUB_PASSWORD: 'your_docker_hub_password'
  AZURE_SUBSCRIPTION_ID: 'your_azure_subscription_id'
  AZURE_RESOURCE_GROUP: 'your_azure_resource_group'
  AZURE_WEBAPP_NAME: 'your_azure_webapp_name'

steps:
- task: Docker@2
  inputs:
    command: 'build'
    containerImage: $(DOCKER_HUB_USERNAME)/node-app:latest
    dockerfile: 'Dockerfile'
- task: Docker@2
  inputs:
    command: 'push'
    containerImage: $(DOCKER_HUB_USERNAME)/node-app:latest
    registry: 'dockerhub'
    username: $(DOCKER_HUB_USERNAME)
    password: $(DOCKER_HUB_PASSWORD)
- task: AzureWebAppDeployment@2
  inputs:
    azureSubscription: $(AZURE_SUBSCRIPTION_ID)
    resourceGroupName: $(AZURE_RESOURCE_GROUP)
    appName: $(AZURE_WEBAPP_NAME)
    package: '$(System.DefaultWorkingDirectory)/app/build'

tasks 27

FROM httpd:latest

COPY index.html /var/www/html/

<!DOCTYPE html>
<html>
<head>
  <title>Hello Apache</title>
</head>
<body>
  <h1>Hello, Apache!</h1>
</body>
</html>

docker build -t apache-hello .
docker run -d -p 80:80 apache-hello

tasks 28

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY FILE 

CMD ["pytest"]

docker build -t python-test .
docker run -it python-test


tasks 29

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY FILE 

CMD ["python", "app.py"]

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello from Flask!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)

    apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: flask-app
  template:
    metadata:
      labels:
        app: flask-app
    spec:
      containers:
      - name: flask-app
        image: your_docker_hub_username/flask-app:latest
        ports:
        - containerPort: 8080

        # Построить образ Docker
docker build -t your_docker_hub_username/flask-app:latest .

# Отправить образ в Docker Hub
docker push your_docker_hub_username/flask-app:latest

# Развернуть приложение в Kubernetes
kubectl apply -f deployment.yaml

tasks 30

FROM python:3.9-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY FILE 

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]



version: '3.7'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db

  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"

docker-compose up -d
