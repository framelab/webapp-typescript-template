FROM ubuntu:latest

MAINTAINER "Ralph Wiedemeier" <ralph@framefactory.ch>
LABEL description="Ubuntu Node Server"
LABEL version="0.2"

# Install provisioning scripts
COPY *.sh /var/provisioning/
WORKDIR /var/provisioning

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y apt-utils \
 && apt-get install -y dos2unix \
 && dos2unix *

# Run provisioning scripts
RUN bash -C './install.sh'

# Set startup directory
WORKDIR /app

# Cleanup
RUN apt-get -y autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# Entrypoint
CMD bash -C '/var/provisioning/run.sh'