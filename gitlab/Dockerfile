FROM forsrc/raspbian:docker

RUN apt-get -q update

RUN apt-get install -y curl

RUN curl -s https://packages.gitlab.com/install/repositories/gitlab/raspberry-pi2/script.deb.sh | bash

RUN apt-get install -y runit-systemd gitlab-ce

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN echo ' \n\
if [ ! -f /usr/lib/systemd/system/gitlab-runsvdir.service ]; then \n\
    gitlab-ctl reconfigure \n\
    systemctl enable gitlab-runsvdir.service \n\
    systemctl start gitlab-runsvdir.service \n\
fi \n\
/opt/gitlab/embedded/bin/runsvdir-start' > /endpoint.sh

RUN chmod +x /endpoint.sh

RUN cat /endpoint.sh
#VOLUME /etc/gitlab
VOLUME /var/log/gitlab
VOLUME /var/opt/gitlab/git-data

EXPOSE 443 80 22

CMD ["/endpoint.sh"]
