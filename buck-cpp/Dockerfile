FROM openjdk:8

MAINTAINER nickersoft@gmail.com

#################################
#     INSTALLING THE BASICS     #
#################################

# Switch to the root user
USER root

# Update apt-get and install missing software
RUN apt-get -y update
RUN apt-get -y upgrade

# Install C/C++ dependencies
RUN apt-get -y install gcc g++ make cmake clang wget curl build-essential

# Install Watchman dependencies
RUN apt-get -y install libssl-dev autoconf automake libtool pkg-config

# Install Buck dependencies
RUN apt-get -y install git ant python python-dev

###############################
#     INSTALLING WATCHMAN     #
###############################

# Clone the Watchman repo to /watchman
RUN git clone https://github.com/facebook/watchman.git /watchman/

# Change the working directory to /watchman
WORKDIR /watchman

# Checkout the latest stable version (v4.9.0 as of March 27, 2018)
RUN git checkout v4.9.0

# Run Watchman make commands
RUN ./autogen.sh 
RUN ./configure
RUN make
RUN make install

###########################
#     INSTALLING BUCK     #
###########################

# Clone the Buck repo to /buck
RUN git clone https://github.com/facebook/buck.git /buck/

# Change the working directory to /buck
WORKDIR /buck

# Build Buck
RUN ant

# Create a symlink in /usr/bin that points to /buck/bin/buck
RUN ln -sf /buck/bin/buck /usr/bin/
