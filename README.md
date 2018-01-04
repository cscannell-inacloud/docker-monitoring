![Grafana](https://i.imgur.com/7ToLMQi.png) ![Prometheus](https://i.imgur.com/i5injY1.png) ![cAdvisor](https://i.imgur.com/NLoyfdy.png)

# Easy Monitoring - Grafana + Prometheus + cAdvisor
So, you want to know about your Docker setup performance but you don't really know how to do it or you'd rather want to invest your time in more important tasks? Here's an easy and fast solution!

With this project, you'll be able to generate a configuration adapted to your environment and create & run cAdvisor, Prometheus and Grafana using docker-compose as well as a .service file.

## Installation Guide

### Pre-requisites
To use this project, you'll need the following installed on your host machine:
- [Docker](https://www.docker.com/get-docker)
- [Ansible](https://www.ansible.com/)
- [Docker-compose](https://docs.docker.com/compose/install/)
- [Systemd](https://wiki.archlinux.org/index.php/systemd)

### Set up your environment in the vars file!
Before you start running the Ansible playbook, make sure you setup the *vars.yml* file (down *vars* folder!). This file has its variable sets commented, so you know what each of them is for.

### Time to run our playbook!
Once you've set up your environment, it's time to run the playbook. Do so by running the following command where the *playbook.yml* is located:

`ansible-playbook playbook.yml`

### Explaining the setup
This playbook will create the folder where the docker-compose file will be located, along with the Dockerfiles of Prometheus & Grafana containers; then it'll copy the files to that folder and finally it'll run the newly created service to start the three containers.

Once the process is finished, you'll have the three containers running, and you'll be able to access to Grafana using the IP of the host machine along with the desired port.

You'll also be able to check on cAdvisor metrics, installed in the same host machine as Prometheus. To achieve this, the docker-compose file will create an internal network, which Prometheus will use to contact with cAdvisor metrics endpoint and retrieve all the metrics, so Grafana can use them.

This should be done this way, as Docker containers can't '*curl*' the host machine IP, as it's not recognized.

### How does it look?
The following image features a setup where Prometheus is looking at metrics extracted from two containers which uses tomcat to run a JAVA application. Those metrics are from the JVMs running inside those containers.

To achieve this specific setup, you'll need a jmx_exporter to serve the metrics, as well as activate jmxremote in the JAVA_OPTS.

![Dashboard](https://i.imgur.com/pMEQVjd.png)
