FROM forsrc/raspbian

RUN apt-get -q update

RUN apt-get install -y python python-pip python3 python3-pip

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

WORKDIR /home/pi

RUN curl -k https://bootstrap.pypa.io/get-pip.py -o get-pip.py
#RUN python get-pip.py
RUN python3 get-pip.py

#CMD ["/sbin/init"]
