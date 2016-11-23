# set base os
FROM phusion/baseimage:0.9.16
ENV DEBIAN_FRONTEND noninteractive
# Set correct environment variables
ENV HOME /root
ENV TERM xterm
# Configure user nobody to match unRAID's settings
RUN \
usermod -u 99 nobody && \
usermod -g 100 nobody && \
usermod -d /home nobody && \
chown -R nobody:users /home && \

#Install Asset-upnp
apt-get update && \
mkdir -p /usr/bin/asset && \
chmod -R 777 /usr/bin/asset

#Unpack our premium version
ADD AssetUPnP-Linux-x64-premium.tar.gz /usr/bin/asset/

RUN \
apt-get autoremove -y && \
apt-get clean && \
mkdir /config && \
ln -s /config /root/.dBpoweramp
VOLUME /config
VOLUME /music
EXPOSE 45537/tcp 26125/tcp 1900/udp
ENTRYPOINT ["/usr/bin/asset/bin/AssetUPnP"]
root@Tower:/mnt/user/Useful/Dockers/assetupnp# vi Dockerfile
reading Dockerfile
