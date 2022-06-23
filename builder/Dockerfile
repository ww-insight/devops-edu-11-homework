FROM ubuntu
RUN apt update
RUN apt install default-jdk -y
RUN apt install maven -y
RUN apt install git -y
RUN apt install docker.io -y
RUN chmod 666 /var/run/docker.sock
RUN service docker restart