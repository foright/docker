FROM ubuntu:14.04
MAINTAINER ccqngu@gmail.com

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:123456' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN apt-get install -y zsh
RUN apt-get install -y tmux
RUN apt-get install -y vim
RUN apt-get install -y nginx
RUN apt-get install -y php5.6
RUN apt-get install -y curl
RUN apt-get install -y mysql-server
RUN apt-get install -y sshpass
RUN curl https://j.mp/spf13-vim3 -L > spf13-vim.sh && sh spf13-vim.sh

EXPOSE 22 80 3306
CMD ["/usr/sbin/sshd", "-D"]