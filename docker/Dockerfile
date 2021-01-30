FROM forsrc/raspbian

RUN apt-get update

WORKDIR /home/pi


RUN curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

RUN systemctl anable docker

VOLUME /var/lib/docker

EXPOSE 2375 2376

