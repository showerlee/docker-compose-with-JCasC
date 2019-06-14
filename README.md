# Jenkins cluster with JCasC via docker swarm

## Docker Version Support

Docker client: 17.06.0+

Docker swarm: 17.06.0+

## Build docker images
```
cd compose/jenkins/
docker build -t showerlee/jenkins:2.164.1 .
cd compose/jenkins-slave-ssh/
docker build -t showerlee/jenkins-slave:2.164.1 .
```

## Start Jenkins cluster via docker swarm(1 master and 2 slaves)
```
cd compose/
docker stack deploy -c stack.yml jenkins
```


## Links

* https://github.com/jenkinsci/docker/blob/master/README.md

* http://tdongsi.github.io/blog/2017/12/30/groovy-hook-script-and-jenkins-configuration-as-code/

* https://github.com/openfrontier/docker-jenkins/tree/master/init.groovy.d

* https://technologyconversations.com/2017/06/16/automating-jenkins-docker-setup/


## Plugin Links

* https://github.com/jenkinsci/configuration-as-code-plugin

* https://wiki.jenkins.io/display/JENKINS/Docker+Plugin

* https://github.com/jenkinsci/docker-swarm-plugin
