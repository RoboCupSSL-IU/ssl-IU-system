# set the base image
FROM dorowu/ubuntu-desktop-lxde-vnc:bionic-lxqt
#FROM ubuntu:18.04

# author
MAINTAINER Hany Hamed

# extra metadata
LABEL version="0.1"
LABEL description="Docker image for grsim to run without any problems in compiling"

#RUN useradd -ms /bin/bash IU

#RUN apt-get install -y sudo && \
#    adduser rc_ssl_iu && \
#    echo "rc_ssl_iu ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/rc_ssl_iu && \
#    chmod 0440 /etc/sudoers.d/rc_ssl_iu

#RUN su - rc_ssl_iu -c "touch mine"

#CMD ["su", "-", "rc_ssl_iu", "-c", "/bin/bash"]

#USER RC_SSL_IU
#ENV HOME /home/RC_SSL_IU
RUN mkdir /home/RC_SSL_IU
WORKDIR /home/RC_SSL_IU
#WORKDIR ~
#WORKDIR /home

# update sources list
RUN apt-get -qy update

# Install the required dependencies
RUN apt-get -qy install git build-essential cmake qt5-default libqt5opengl5-dev libgl1-mesa-dev libglu1-mesa-dev libprotobuf-dev protobuf-compiler libboost-dev

RUN apt-get -qy install libode-dev tar wget pkg-config

RUN wget https://bitbucket.org/odedevs/ode/downloads/ode-0.16.tar.gz
RUN tar xvf ode-0.16.tar.gz
RUN cd ode-0.16 && ./configure --enable-double-precision
RUN cd ode-0.16 && make && make install
#RUN cd /etc/ld.so.conf.d && echo "/home/ode-0.16/build/lib" > myLibs.conf
RUN ldconfig
RUN pkg-config ode --cflags
RUN pkg-config ode --libs
#RUN export ODE_DIR=”/home/ode-0.16/build”
#RUN echo "export ODE_DIR=”/home/ode-0.16/build” > ~/.bashrc

RUN git clone https://github.com/jpfeltracco/vartypes.git
# RUN cd vartypes
RUN cd vartypes && mkdir build && cd build && cmake .. && make && make install
# RUN cmake ..
# RUN make
# RUN make install

RUN git clone --recursive https://github.com/RoboCupSSL-IU/SSL-IU-system.git

RUN cd SSL-IU-system/grSim && mkdir build && cd build && cmake .. && make


RUN apt-get -qy update --fix-missing

RUN cd SSL-IU-system/ssl-vision && ./InstallPackagesUbuntu.sh &&\
    mkdir build && cd build && cmake -DUSE_V4L=true .. && cd .. && make

