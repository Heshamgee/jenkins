FROM centos:7

# Install bind-utils (includes nslookup)
RUN yum -y install bind-utils

# Add custom DNS server
RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf

# Update repository URLs to use vault.centos.org
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

# Install openssh-server
RUN yum -y install openssh-server

RUN useradd hesham-remote && \ 
    echo"hesham-remote:hesham" | chpasswd && \
    mkdir /home/hesham-remote/.ssh && \ 
    chmod 700 /home/hesham-remote/.ssh

COPY remote-key.pub /home/hesham-remote/.ssh/authorized_keys 
RUN chown hesham-remote:hesham-remote -R /home/hesham-remote/.ssh/ && \
    chmod 600 /home/hesham-remote/.ssh/authorized_keys
RUN /usr/sbin/sshd-keygen
CMD /usr/sbin/sshd -D 
