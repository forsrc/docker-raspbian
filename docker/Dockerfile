FROM forsrc/raspbian:systemd

RUN apt-get -q update

RUN apt-get install -y curl

WORKDIR /home/pi


RUN curl -k https://get.docker.com -o get-docker.sh
RUN chmod +x get-docker.sh
RUN ./get-docker.sh

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN systemctl enable docker

VOLUME /var/lib/docker

EXPOSE 2375 2376

CMD ["/sbin/init"]
