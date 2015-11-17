# Kubernetes Using Docker-Compose and Docker-Machine On OSX

Contained is a docker-compose file that will get [Kubernetes](http://kubernetes.io/) up and running locally on OSX. Majority of this comes from the official Kubernets information located here: http://kubernetes.io/v1.0/docs/getting-started-guides/docker.html
	
## Get Kubernets Running Locally

To get Kubernets running locally on Mac OSX, follow the below steps and it should be up and running in no time.


### Install Kubectl

Next we need to get the Kubectl binary installed locally.

```sh
$ curl -O https://storage.googleapis.com/kubernetes-release/release/v0.18.2/bin/darwin/amd64/kubectl
$ chmod +x kubectl
$ mv kubectl /usr/local/bin/
```

To ensure that `kubectl` is installed correctly, issue the following command and make sure the output is correct.

```sh 
$ which kubectl
/usr/local/bin/kubectl
```

### Clone the Repo

You'll need to clone the repo so you get the `docker-compose.yml` file.

```sh
$ git clone git@github.com:mtahv3/kubernetes-compose.git
```

### Start Kubernetes

Now that we have everything ready locally, we can fire up Kubernetes using `docker-compose` issue the following commands in terminal

```sh
$ docker-compose -f /path/to/cloned/repo/kubernetes-compose/docker-compose.yml up -d
```

This should fire up the needed Docker containers to get Kubernetes running. However, since we're using docker machine and are not actually logged into the machine running docker, we need to setup port forwarding so our calls to the Kubernetes API get forwarded along accordingly.

