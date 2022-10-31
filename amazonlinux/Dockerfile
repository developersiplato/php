FROM amazonlinux:latest

RUN yum update -y
RUN yum install -y make gcc automake mysql-devel jansson-devel openssl11-libs

RUN yum groupinstall -y 'Development Tools'

RUN rpm --install https://vault.centos.org/centos/8/BaseOS/x86_64/os/Packages/librabbitmq-0.9.0-3.el8.x86_64.rpm
RUN rpm --install https://vault.centos.org/centos/8/PowerTools/x86_64/os/Packages/librabbitmq-devel-0.9.0-3.el8.x86_64.rpm