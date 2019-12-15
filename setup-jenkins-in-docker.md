# Getting Started

## Step 1: Start jenkins using docker

Here we use docker volume to give access the docker.sock, That will help to manage docker inside docker.

Docker run command:

```sh
docker run -d -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):$(which docker) -p 8080:8080 -p 50000:50000 --name jenkins-docker jenkins/jenkins:lts
```

Add permission `/var/run/docker.sock`

```sh
docker exec -it -u root jenkins-docker /bin/bash

$ groupadd docker
$ chmod 777 /var/run/docker.sock
```

## Step 2: Add Docker plugin in jenkins

Manage Jenkins > Manage Plugins > Available (tab) > Search 'Docker' > tick the checkbox > click 'Download now and install after restart'

## Step 3: Configure docker in jenkins

Manage Jenkins > Configure System > Cloud (Section) > Add a new Cloud

Name: `Docker`

Docker Host URI:`unix:///var/run/docker.sock`

Enabled: `Checked`

Click `Test connection`
