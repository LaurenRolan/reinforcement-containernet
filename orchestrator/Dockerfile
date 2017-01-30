# Build with $ sudo docker build -t firewall .
# Python files must be in the same folder as Dockerfile
# Run with $ sudo docker run --privileged=true --name my_instance -i -t firewall
# More: https://www.digitalocean.com/community/tutorials/docker-explained-using-dockerfiles-to-automate-building-of-images

FROM ubuntu:latest

RUN su && apt-get update

RUN apt-get install sudo iptables bridge-utils ebtables -y
