FROM rancher/os-alpineconsole-base
# FROM amd64=alpine:3.8 arm64=arm64v8/alpine:3.8
RUN apk --no-cache add bash openssh iptables rsync sudo vim less curl ca-certificates htop kmod iproute2 util-linux bash-completion
# missing packages at 2016-Nov: locales psmisc
RUN rm -rf /etc/ssh/*key*
#RUN locale-gen en_US.UTF-8
RUN addgroup -g 1100 rancher && \
    addgroup -g 1101 docker && \
    addgroup -S sudo && \
    adduser -D -u 1100 -g rancher -G sudo -s /bin/bash rancher && \
    adduser rancher docker && \
    adduser -D -u 1101 -g docker -G sudo -s /bin/bash docker && \
    adduser docker docker && \
    sed -i 's/rancher:!/rancher:*/g' /etc/shadow && \
    sed -i 's/docker:!/docker:*/g' /etc/shadow && \
    echo ClientAliveInterval 180 >> /etc/ssh/sshd_config && \
    echo '## allow password less for rancher user' >> /etc/sudoers && \
    echo 'rancher ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo '## allow password less for docker user' >> /etc/sudoers && \
    echo 'docker ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    echo 'ssh-keygen -A' >> /usr/sbin/update-ssh-keys && \
    ln -s /bin/ps /usr/bin/ps
ENTRYPOINT ["/usr/bin/ros", "entrypoint"]
