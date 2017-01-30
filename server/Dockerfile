# Build with $ sudo docker build -t server .
# Python files must be in the same folder as Dockerfile
# Run with $ sudo docker run --name my_instance -i -t server
# More: https://www.digitalocean.com/community/tutorials/docker-explained-using-dockerfiles-to-automate-building-of-images

FROM ubuntu:latest

RUN su && apt-get update

RUN apt-get install sudo python -y

ADD server.py ./home

ADD 50mb.flv ./home
