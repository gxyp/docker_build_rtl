# The dockerfile has Change add sshd services on Centos7.1
FROM centos:7.1.1503

MAINTAINER guozhen,https://?????

#Clean tmp
RUN rm -rf /var/lib/rpm/__db.* \
 && yum clean all \
 && yum makecache -y \

#Install develop env
 && rpm --rebuilddb && yum install -y openssh-server glibc gcc bc \
 && rpm --rebuilddb && yum install zlib zlib-devel zlib.i686 zlib-devel.i686 -y \
 && rpm --rebuilddb && yum install bison flex gawk cmake automake make -y \
 && rpm --rebuilddb && yum install compat-libstdc++-296.i686 compat-libstdc++-33.i686 -y \
 && rpm --rebuilddb && yum install xz-devel bsdtar glibc-devel glibc-devel.i686 -y \
 && rpm --rebuilddb && yum swap -y fakesystemd systemd && yum install -y systemd-devel \
 && rpm --rebuilddb && yum update -y libstdc++.x86_64 && yum install -y libstdc++.i686 \
 && rpm --rebuilddb && yum install -y ncurses-devel ncurses-devel.i686 \

 && rpm --rebuilddb && yum install -y perl bzip2 gcc-c++ lzma-devel gnutils-devel \
 && rpm --rebuilddb && yum install -y bison-devel \

#Set password for root
 && echo 'root:123456' | chpasswd \
 && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \

#Create key
 && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key \

#Set about ssh
    && mkdir /var/run/sshd \
    && sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd \
    && sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

#Open port
EXPOSE 22

#Set history record
ENV HISTTIMEFORMAT "%F %T  "

ADD run.sh /usr/local/sbin/run.sh
RUN chmod +x /usr/local/sbin/run.sh

#Auto running some service
CMD ["/usr/local/sbin/run.sh"]
