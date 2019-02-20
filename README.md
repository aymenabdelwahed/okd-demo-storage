# okd-demo-storage

Demo of various storage backend used into OKD

## Install startx-demo script

```bash
#switch to root user
sudo su -
#Download startx-demo script
curl -s https://goo.gl/4FJs3u > /usr/bin/startx-demo > /usr/local/bin/startx-demo
#Allow script execution
chmod ugo+x /usr/local/bin/startx-demo
#Start dependencies installation
startx-demo install
```

## Setup demo environment

```bash
#login to openshift cluster (interactive)
startx-demo login force
#setup and create the openshift project to use (interactive)
startx-demo project force
#load images streams and templates
startx-demo load
#list generic ressources in project
startx-demo get
```

## Excute ephemeral demo

```bash
#start the ephemeral demo
startx-demo ephemeral start
#watch openshift ressources and storage content for the ephemeral demo (dynamic)
startx-demo ephemeral watch
#show openshift ressources for the ephemeral demo
startx-demo ephemeral ps
#show storage content for the ephemeral demo
startx-demo ephemeral ls
#delete openshift ressources and storage content for the ephemeral demo (asynchronous)
startx-demo ephemeral delete
```

## Excute volatile demo

```bash
#start the volatile demo
startx-demo volatile start
#watch openshift ressources and storage content for the volatile demo (dynamic)
startx-demo volatile watch
#show openshift ressources for the volatile demo
startx-demo volatile ps
#show storage content for the volatile demo
startx-demo volatile ls
#delete openshift ressources and storage content for the volatile demo (asynchronous)
startx-demo volatile delete
```

## Excute resilient demo

```bash
#start the resilient demo
startx-demo resilient start
#watch openshift ressources and storage content for the resilient demo (dynamic)
startx-demo resilient watch
#show openshift ressources for the resilient demo
startx-demo resilient ps
#show storage content for the resilient demo
startx-demo resilient ls
#delete openshift ressources and storage content for the resilient demo (asynchronous)
startx-demo resilient delete
```

## Excute distributed demo

```bash
#start the distributed demo
startx-demo distributed start
#watch openshift ressources and storage content for the distributed demo (dynamic)
startx-demo distributed watch
#show openshift ressources for the distributed demo
startx-demo distributed ps
#show storage content for the distributed demo
startx-demo distributed ls
#delete openshift ressources and storage content for the distributed demo (asynchronous)
startx-demo distributed delete
```


## close this demo

```bash
#remove all resource and project
startx-demo delete
```

