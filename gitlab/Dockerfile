FROM forsrc/raspbian:docker

RUN apt-get -q update

RUN apt-get install -y curl

RUN curl -s https://packages.gitlab.com/install/repositories/gitlab/raspberry-pi2/script.deb.sh | bash

RUN apt-get install -y gitlab-ce

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN cat > > /endpoint.sh <<EOF 
#!/bin/sh
if [ ! -f /usr/lib/systemd/system/gitlab-runsvdir.service ]; then
    gitlab-ctl reconfigure
    systemctl enable gitlab-runsvdir.service
    systemctl start gitlab-runsvdir.service
fi

exec "$@"
EOF


#VOLUME /etc/gitlab
VOLUME /var/log/gitlab
VOLUME /var/opt/gitlab/git-data

EXPOSE 443 80 22

ENTRYPOINT ["/endpoint.sh"]
