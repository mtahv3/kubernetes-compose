# Kubernetes Using Docker-Compose and Docker-Machine On OSX

Contained is a docker-compose file that will get [Kubernetes](http://kubernetes.io/) up and running locally on OSX. Majority of this comes from the official Kubernets information located here: http://kubernetes.io/v1.0/docs/getting-started-guides/docker.html
	
## Get Kubernets Running Locally

To get Kubernets running locally on Mac OSX, follow the below steps and it should be up and running in no time.


### Install Kubectl

First we need to get the Kubectl binary installed locally.

```sh
$ curl -O https://storage.googleapis.com/kubernetes-release/release/v1.1.1/bin/darwin/amd64/kubectl
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

```sh
$ docker-machine ssh $(docker-machine active) -f -N -L 8080:localhost:8080
```

### Test It Out

Assuming the above went smoothly, you can test it out by issuing the following command on your local OSX terminal. You should see the following output. 

```sh
$ kubectl get nodes
NAME        LABELS                             STATUS    AGE
127.0.0.1   kubernetes.io/hostname=127.0.0.1   Ready     17m
```

_Note: it may take a few seconds for Kubernetes to get everything up and running. If you see issues about not being able to connect on 127.0.0.1 or EOF, wait a few seconds and try again._

### Shortcuts

The following aliases can be added to your bash profile to make getting Kubernetes up and running even quicker. Assuming the above works, you can add the following.

```sh
$ echo "alias kubeup='docker-compose -f /full/path/to/cloned/repo/kubernetes-compose/docker-compose.yml up -d && docker-machine ssh $(docker-machine active) -f -N -L 8080:localhost:8080'" >> ~/.bash_profile
```

This will add a command called `kubeup` to your bash profile which will start Kubernetes using docker-compose and create the necessary port forwardings.

To get the command working, either restart your terminal, or issue the following command.

```sh
$ source ~/.bash_profile
```

To use the command it's as simple as doing

```sh
$ kubeup
Creating kubernetescompose_master_1
Creating kubernetescompose_proxy_1
Creating kubernetescompose_etcd_1
```

## Troubleshooting

### Conflicting Port 8080

Make sure that port 8080 isn't already in use by some other application - if so, then Kubernetes API cannot connect on that port.

### Check the logs

Log files are always a good place to get information. Use the following command to check the log files.

```sh
$ docker logs kubernetescompose_master_1
```

Or using any container name from running `docker ps`

