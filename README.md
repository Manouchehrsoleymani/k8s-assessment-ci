# Distribution traffice assessment-CI
In this repository, we are going to **develop**  a new versions of the application and **build** the Image then push it into **Docker hub** registry
## How it works
The project has an index.html file and content includes:
### Container - nginx-v1

    index.html
    I'm version v1!

another constraint is use **nginx:1.24.0** for base Image.

To simplify we use **appv1**  for the application's names. 
we are going to change index file like :
### Container - nginx-v2

    index.html
    I'm version v2!

For Countinuse integration, we use **github Action**  to build a new images with github hash as a tage then push them into the registry. there are 4 steps to build images and push.

 - **Checkout** :This action checks-out your repository under `$GITHUB_WORKSPACE`, so your workflow can access it.
 - **Scan Dockerfile using Checkov** : Checkov scans cloud infrastructure configurations to find misconfigurations/security policies before they're deployed
 - **Login to Docker Hub** : add credentials  to establish a connection to Docker hub
 - **Build & push container image**: build the image based on the Docker file and push it into the Docker hub
 there are some conditions to build a new image and push it into the docker registry that we define in GitHub action yaml file. as you can see below if somebody modifies the README.md file, it doesn't need to build a new image. or for small changes, there is no tag to push to the GitHub repository, so when you assign a tag to your changes or do some modification on the app folder, GitHub action will be triggered.

> on:
      push:
        tags:
        - "*"
        paths:
        - appv2/*
## How to build images locally

    https://github.com/Manouchehrsoleymani/k8s-assessment-ci.git
    cd k8s-assessment-ci
    docker build -t manouchehrsolamani:v1 appv1/

To run locally :

    
    docker run --name appv1 -p 8080:80 manouchehrsolamani/trivago:v1
    
To push into registry:

> `docker push <your-account>/<repository-name>:<tag>`

    Docker login
    docker push manouchehrsolamani/trivago:v1
    
 *Ensure that you have to make a repository befor push image*
 
 To pull images form registry:
 

    docker pull manouchehrsolamani/trivago:v1
