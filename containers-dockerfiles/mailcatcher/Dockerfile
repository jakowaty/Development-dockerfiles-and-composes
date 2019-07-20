FROM debian:latest

RUN apt-get -y update && apt-get -y upgrade&& \
apt-get -y install ca-certificates openssl ruby sqlite libstdc++ ruby-dev make ruby-json libsqlite3-dev g++ && \
gem install mailcatcher --no-ri --no-rdoc

EXPOSE 1025 1080

CMD ["mailcatcher", "--foreground", "--ip=0.0.0.0"]

