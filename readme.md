## 1. Install Docker Host

https://docs.docker.com/docker-for-mac/install/

## 2. Start and Configure the Jenkins Server

```
# creates the internal docker network
docker network create jenkins

# pull and start the jenkins docker image
docker pull jenkins/jenkins:lts
docker run -p 8080:8080 -p 50000:50000 --network jenkins --hostname jenkins jenkins/jenkins:lts
```

## 3. Create the devenv Docker Container

```
docker build -t 'devenv' . 
docker run -d -p 8090:8080 -p 3001:22 --name devenv --network jenkins --hostname devenv devenv:latest
```

## 4. Configure devenv container as docker-slave

#### 4.1 go to manage jenkins
![Manage Jenkins](/images/1.png)

#### 4.2 go to manage nodes
![Manage Nodes](/images/2.png)

#### 4.3 go to New Node 

#### 4.4 configure the node
![Slave Config](/images/3.png)

#### 4.5 add credentials for jenkins to use the slave node
![Creds](/images/4.png)

## 5. Create a multibranch pipeline for the project

#### 5.1 Configure the job
![pipeline config](/images/5.png)

#### 5.2 point to git repo https://github.com/D3adlock/cicd-pipeline-handson-code
![pipeline config](/images/6.png)
# cicd-pipeline-handson-code
