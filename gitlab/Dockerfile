FROM forsrc/raspbian:docker

RUN apt-get -q update

RUN apt-get install -y curl

RUN curl -s https://packages.gitlab.com/install/repositories/gitlab/raspberry-pi2/script.deb.sh | bash

RUN apt-get install -y runit-systemd gitlab-ce

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN echo ' \n\
systemctl mask systemd-firstboot.service systemd-udevd.service systemd-modules-load.service \n\
systemctl unmask systemd-logind \n\
if [ ! -f /opt/gitlab/dind_init ]; then
    echo =================
    gitlab-ctl reconfigure &
    sleep 120
    echo =================
    gitlab-ctl start
    touch /opt/gitlab/dind_init
    echo =================
fi
echo start ... \n\
(sleep 3 && /opt/gitlab/embedded/bin/runsvdir-start) & \n\

if [[  "$@" != "" ]] ; then \n\
    exec "$@" \n\
else \n\
    exec /sbin/init \n\
fi ' > /endpoint.sh


RUN chmod +x /endpoint.sh

RUN cat /endpoint.sh
#VOLUME /etc/gitlab
VOLUME /var/log/gitlab
VOLUME /var/opt/gitlab/git-data

EXPOSE 443 80 22

CMD ["/endpoint.sh"]
