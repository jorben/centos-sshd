FROM centos:6.6
MAINTAINER jorben <jorben@users.noreply.github.com>
RUN yum install -y openssh-server openssh-clients
RUN echo 'root:root@1234' | chpasswd
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN /sbin/service sshd start && /sbin/service sshd stop

RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -ivh epel-release-6-8.noarch.rpm
RUN yum install -y libnet libpcap libnet-devel libpcap-devel

RUN git clone https://github.com/snooda/net-speeder.git net-speeder
WORKDIR net-speeder
RUN sh build.sh

RUN mv net_speeder /usr/local/bin/
RUN chmod +x /usr/local/bin/net_speeder
RUN nohup /usr/local/bin/net_speeder venet0 "ip" >/dev/null 2>&1
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
