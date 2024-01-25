# CentOS7
FROM amazonlinux:latest

# install ssh server
RUN yum -y install sudo openssh-server openssh-clients which vim && yum clean all

# create Public key
RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa
RUN ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N '' -t ecdsa

# rootでのパスワードなしでのsshgログインを許可する
RUN sed -ri 's/^PermitEmptyPasswords no/PermitEmptyPasswords yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^#PermitRootLogin prohibit\-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

# set a password for root
RUN echo "root:" | chpasswd
#RUN adduser -p passwd -U root test

# expose 22 port
EXPOSE 22

# start up sshd
CMD ["/usr/sbin/sshd", "-D"]
