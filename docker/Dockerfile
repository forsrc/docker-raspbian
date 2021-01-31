FROM forsrc/raspbian

RUN apt-get -q update

RUN apt-get install -y curl systemd init

WORKDIR /home/pi


RUN curl -k https://get.docker.com -o get-docker.sh
RUN chmod +x get-docker.sh
RUN ./get-docker.sh

RUN systemctl enable docker

VOLUME /var/lib/docker

EXPOSE 2375 2376

CMD ["/sbin/init"]
