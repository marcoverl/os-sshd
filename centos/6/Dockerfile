FROM centos:6

RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all

#Pre-installed packages to speed IM contextualization
RUN yum -y install \
    openssh \
    openssh-clients \
    openssh-server \
    python-distribute \
    gcc \
    python-devel \
    wget \
    openssh-client \
    sshpass \
    ansible \
    && yum clean all

RUN easy_install pip

RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa

RUN ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N '' -t ecdsa

RUN echo "root:indig0!" | chpasswd

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
