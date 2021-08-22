Welcome to the ruby-web-server-minikube-ansible wiki!

# **Containerize and Deploymet to Kubernetes using Ansible**

This is meant for minikube CI/CD deployment. 
Can be used to dev/test grade Kubernetes (k8s) as well with small tweaks in the "ansible-main.yaml"

## **Application Used:**
Ruby [Simple Ruby Web Server](https://github.com/sawasy/http_server)
It runs on TCP port 80. The application also exposes a health check and endpoint at the route /healthcheck.

Pre-Requsites to be installed on host machine: (Ubuntu 20.04.3 LTS)
Ansbile
Minikube
Docker
kubectl (CLI)

***

## **Important Files:**

1) **_deployment-using-ansible-shell-main.yaml_** - This playbook will use Linux's native shell method to deploy deployment in minikube/k8s.
2) **_deployment-using-ansible-module-main.yaml_** - This deployment will use Ansible's K8s module to deploy deployment in minikube/k8s. Please refer collection installation method to use this playbook.
2) _**vars/kube-vars.yaml**_ - variables that determine our service specific items, like ports, container image, tag, etc within the kubernetes template or application/deployment.
3) _**templates/kube_deployment.yml**_ - This is a base template used to create a basic kubernetes deployment and pod.
4) _**http_server.rb**_ - This is a simple ruby based web service. Refer "Application Used" section for more info.
4) _**Dockerfile**_ - This file will create a docker image with http_server.rb and expose the app on port "80".

***

## **Dependencies Installation:**

Ansible Installation: (Below Steps for Ubuntu 20.04.3 LTS)
###   
     $ pip install ansible-base
     $ sudo apt update`
     $ sudo apt install software-properties-common`
     $ sudo add-apt-repository --yes --update ppa:ansible/ansible`
     $ sudo apt install ansible`
     $ sudo ansible-galaxy collection install kubernetes.core`
     $ sudo ansible-galaxy collection install community.kubernetes`

Make sure to install Ansible version 2.10.13 or above. To upgrade from lower version to 2.10, please refer [Ansible Doc's](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pip-upgrade)

Once Ansbile is installed, run below command to install dependencies (Docker, Minikube, Kubectl)
###
    $ ansible-playbook -i host dependency-install.yaml -b -K

This will install Docker, Minikube, Kubectl in your base machine
***
## **How to deploy Ruby Web server in Minikube/k8s:**

1. Make sure you install Ansible, Docker, Minikube and Kubectl in your base machine. 
2. Clone this repository.
3. Update the kube-vars.yml file to match your needs. 
4. Run below ansible command to deploy ruby web server to minikube/k8s

Shell based deployment:
###
    $ ansible-playbook -i host deployment-using-ansible-shell-main.yaml

K8s module based deployment:
###
    $ ansible-playbook -i host deployment-using-ansible-module-main.yaml

***

## **Architecture:**

###
    Ansible - Build & Deployment Tool. Automates the Docker image building and Deployment in Minikube/k8s.
    Docker - Containerzation Tool. Creates a container image with given web app based on the parameters passed in Dockerfile.
    Minikube - Localized platform to run contianer images as kubernetes cluster.

    
