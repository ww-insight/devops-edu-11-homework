FROM ubuntu
RUN apt update
RUN apt install default-jdk -y
RUN apt install maven -y
RUN apt install git -y
RUN apt install docker.io -y
COPY config.json /.docker/config.json
RUN chmod 777 /.docker/config.json