# How-To-Dockerize-NodeJS-Backend

```
Author: BlackLeakz
Name: How To Dockerize Node.JS Server/Backend Application
Version: latest
Website: https://tutorials.blackzspace.de/how-to-docker
Github: https://github.com/blackzspace-de-Tutorials/How-To-Dockerize-NodeJS-Backend.git
Description: Tutorial of how to deploy a docker container including your node.js project! And how to automate-build container by editing build-options in package.json - File!
```


What to you need:

- Docker Engine / Docker Desktop !
- A Ready for Deploy - Node.JS Project !
- 5Minutes of your time!


# 1st:

Login into your docker-account! - with your credentials 

```sh
sudo docker login
```

# 2nd:

CD into your Node.JS Project folder!

```sh
cd ~/path/to/project
```

(# 3rd: -- SEE FOOTER FOR package.json configuration!)

To automatically update your docker-container by "npm run docker-build" command, follow the instructions in package-json - config's README.md!

# 3rd:

To create a docker-container you need to create a Dockerfile, so: 
(REPLACE your EXPOSE PORT WITH THE PORT YOUR SERVER IS RUNNING ON!!!)

```sh
tee -a Dockerfile <<EOF

# syntax=docker/dockerfile:experimental

FROM node:latest

WORKDIR /src/bin/app

COPY . .

RUN npm i

CMD [ "npm", "start" ]

EXPOSE 8081
EOF
```

# 4th:

Now build the image/container by running following command:
(REPLACE USERNAME AND PROJECT/CONTAINER-NAME WITH YOUR CREDENTIALS!!!)

```sh
sudo docker build -t dockerusername/project-name:version . && sudo docker tag dockerusername/project-name:version dockerusername/project-name && sudo docker push dockerusername/project-name:version
```

# FINISHED!

Now you are done! You successfully created a docker-container/image and deployed it to your repository!




# Example package.json for auto-build docker container/image and push to hub.docker.com




# What is the point in this build configuration?

- You can easily build a docker-container from your node.js source-code by just enter: npm run docker-build !


What do you need to do is:
```txt
- Open your projects package.json!
- Point to "scripts": { } - Section!
- And enter following script-option:
```

```json

"docker-build": "sudo docker build -t dockerusername/project-name:version . && sudo docker tag dockerusername/project-name:version dockerusername/project-name && sudo docker push dockerusername/project-name:version"

```

the package.json could look like this:


```json

{
  "name": "blackzspace.de--backend",
  "version": "1.0.0",
  "description": "",
  "main": "app/server/index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/app/server/index.js",
    "docker-build": "sudo docker build -t dockerusername/project-name:version . && sudo docker tag dockerusername/project-name:version dockerusername/project-name && sudo docker push dockerusername/project-name:version"
    
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cookie-parser": "^1.4.6",
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "fs": "^0.0.1-security",
    "https": "^1.0.0",
    "jsonwebtoken": "^9.0.2",
    "mysql": "^2.18.1",
    "rjutils-collection": "^1.8.0"
  }
}

```


# NOTE: Be sure, you have installed all docker- dependencies and you are loggedin as your hub.docker.com user!

You can manually do this by typing:
```sh
root@debian:~$ sudo docker login
```
:: Just enter your credentials!


# To build the container by command, just enter:

```sh
npm run docker-build
```


### For Example Configurations , look into the example_* Files!


#### To build the test-docker container:

```sh
sudo docker build -t username/docker-nodejs-test:latest .
```

# to run the container:

```sh
sudo docker run username/docker-nodejs-test:latest