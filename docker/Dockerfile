#1) 오픈자바와 SSH서버를 통합한 Dockerfile을 만드시오
#설치할 운영체제를 지정한다.
FROM ubuntu

#작업을 진행할 가상OS USER를 지정한다.
USER root

#작성자 정보를 작성한다.
MAINTAINER Foo Bar <foo@bar.com>

#openjdk 및 openssh-server, tar 설치

RUN apt-get update
RUN apt-get install -y openjdk-8-jdk-headless wget openssh-server tar

#ssh 설정
RUN echo "root:training" | chpasswd
RUN sed -i 's/prohibit-password/yes/' /etc/ssh/sshd_config
ADD ssh.tar /root/
RUN chown -R root:root /root/.ssh;chmod -R 700 /root/.ssh
RUN echo "StrictHostKeyChecking=no" >> /etc/ssh/ssh_config
RUN mkdir /var/run/sshd

# 2) 다음요구조건을 만족하도록 코드를 추가하시오
#- wget을 사용해서 https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz를 다운받으시오
#- 압축을 푸시오(tar xvfz 사용)
#- HADOOP_HOME설정
#- PATH추가 ($HADOOP_HOME/bin, $HADOOP_HOME/sbin 추가)

RUN wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
RUN tar xvfz hadoop-1.2.1.tar.gz /usr/local/hadoop

ENV HADOOP_HOME /usr/local/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin


#Startup
ADD start.sh /

## Port 매핑
EXPOSE 22 8088 50070
CMD bash /start.sh
