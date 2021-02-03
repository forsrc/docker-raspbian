FROM forsrc/raspbian

RUN apt-get -q update

RUN apt-get install -y systemd init

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

CMD ["/sbin/init"]
