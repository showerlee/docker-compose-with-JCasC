# Jenkins cluster with Configuration as Code Plugin via docker swarm
The following is how to deploy Jenkins based on human-readable declarative configuration yaml files via docker swarm orchestration, we can treat Jenkins as a cattle rather than a pet to easily build our CI/CD environment.

## Docker Version Support

Docker: 17.06.0+

## Architecture

Docker manager --> Jenkins master

Docker worker1 --> Jenkins slave01

Docker worker2 --> Jenkins slave02

## 0.Establish docker swarm cluster
refer to: http://www.showerlee.com/archives/2842

## 1.Build docker images
```
cd compose/jenkins/
docker build -t showerlee/jenkins:2.164.1 .
cd compose/jenkins-slave-ssh/
docker build -t showerlee/jenkins-slave:2.164.1 .
```
## 2.Set docker swarm node labels
```
docker node update --label-add jenkins=master manager
docker node update --label-add jenkins=slave01 worker1
docker node update --label-add jenkins=slave02 worker2
```

## 3.Rollout Jenkins cluster via docker swarm
```
cd compose/
docker stack deploy -c stack.yml jenkins
```

## 4.Login Jenkins with the following credential
```
curl http://127.0.0.1:20000
# username: admin
# password: admin
```

![Jenkins](https://github.com/showerlee/Jenkins-Pipeline-CI-CD-with-Helm-on-Kubernetes/blob/master/Jenkins/kube-helm-pipeline.png?raw=true "docker-compose-with-JCasC")

## Links

* https://github.com/jenkinsci/docker/blob/master/README.md

* http://tdongsi.github.io/blog/2017/12/30/groovy-hook-script-and-jenkins-configuration-as-code/

* https://github.com/openfrontier/docker-jenkins/tree/master/init.groovy.d

* https://technologyconversations.com/2017/06/16/automating-jenkins-docker-setup/


## Plugin Links

* https://github.com/jenkinsci/configuration-as-code-plugin

* https://wiki.jenkins.io/display/JENKINS/Docker+Plugin

* https://github.com/jenkinsci/docker-swarm-plugin
