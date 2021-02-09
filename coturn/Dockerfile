FROM forsrc/raspbian:systemd

RUN apt-get update

RUN apt-get -y install coturn certbot sqlite libsqlite3-dev

RUN systemctl enable coturn


RUN sed -i 's/#TURNSERVER_ENABLED=1/TURNSERVER_ENABLED=1/g' /etc/default/coturn

RUN mkdir -p /etc/coturn
RUN openssl genrsa -out /etc/coturn/turn_server_pkey.pem 1024
RUN openssl req -new -key /etc/coturn/turn_server_pkey.pem -out /etc/coturn/turn_server.csr -subj /C=CN/O="forsrc"/OU="forsrc"/CN="coturn.forsrc.com"/ST="forsrc"/L="forsrc"
RUN openssl x509 -req -in /etc/coturn/turn_server.csr -signkey /etc/coturn/turn_server_pkey.pem -out /etc/coturn/turn_server_cert.pem

RUN sed -i 's@#cert=/usr\/local/etc/turn_server_cert.pem@cert=/etc/coturn/turn_server_cert.pem@g' /etc/turnserver.conf
RUN sed -i 's@#pkey=/usr/local/etc/turn_server_pkey.pem@pkey=/etc/coturn/turn_server_pkey.pem@g'  /etc/turnserver.conf
RUN sed -i 's@#server-name=blackdow.carleon.gov@server-name=coturn.forsrc.com@g'                  /etc/turnserver.conf
RUN sed -i 's@#realm=mycompany.org@realm=coturn.forsrc.com@g'                                     /etc/turnserver.conf
RUN sed -i 's@#user=username2:password2@user=forsrc:0xd667eb7aa3ebe3af48ee1c3330941e06@g'         /etc/turnserver.conf
RUN sed -i 's@#web-admin@web-admin@g'                                                             /etc/turnserver.conf
RUN sed -i 's@#web-admin-port=8080@web-admin-port=8080@g'                                         /etc/turnserver.conf
RUN sed -i 's@#web-admin-ip=127.0.0.1@web-admin-ip=0.0.0.0@g'                                     /etc/turnserver.conf

RUN sed -i 's@#listening-port=3478@listening-port=3478@g'                                         /etc/turnserver.conf
RUN sed -i 's@#tls-listening-port=5349@tls-listening-port=5349@g'                                 /etc/turnserver.conf

#RUN sed -i 's@#external-ip=60.70.80.91@external-ip=192.168.2.10@g'                                /etc/turnserver.conf




RUN mkdir -p /var/lib/turn/
RUN mkdir -p /var/run/

RUN turnadmin -a -u forsrc -p forsrc -r coturn.forsrc.com && turnadmin -l
RUN turnadmin -A -u forsrc -p forsrc -r coturn.forsrc.com && turnadmin -L

WORKDIR ~
RUN echo "/usr/bin/turnserver -c /etc/turnserver.conf --pidfile /run/turnserver/turnserver.pid" > start_coturn.sh
RUN echo "kill \$(cat /run/turnserver/turnserver.pid)" > stop_coturn.sh
RUN chmod +x *.sh

EXPOSE 3478 3478/udp
EXPOSE 5347 5347/udp

VOLUME ["/var/lib/coturn"]

CMD ["/sbin/init"]
