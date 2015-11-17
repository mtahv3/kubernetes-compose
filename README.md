# Kubernetes Using Docker-Compose On OSX

Contained is a docker-compose file that will get [Kubernetes](http://kubernetes.io/) up and running locally on OSX. Majority of this comes from the official Kubernets information located here: http://kubernetes.io/v1.0/docs/getting-started-guides/docker.html
	
## Get Kubernets Running Locally

To get Kubernets running locally on Mac OSX, follow the below steps and it should be up and running in no time.


### Clone the Repo

You'll need to clone the repo so you get the `docker-compose.yml` file.

```sh
$ git clone git@github.com:mtahv3/kubernetes-compose.git
```

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

