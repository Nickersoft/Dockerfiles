FROM openjdk:11

MAINTAINER nickersoft@gmail.com

ENV BAZEL_VERSION=2.2.0

#################################
#     INSTALLING THE BASICS     #
#################################

# Switch to the root user
USER root

# Update apt-get and install missing software
RUN apt-get update
RUN apt-get install -y git python python-dev maven curl pkg-config zip g++ zlib1g-dev unzip

############################
#     INSTALLING BAZEL     #
############################

# Download the install script
RUN curl -L https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh > ./bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh
RUN chmod +x bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh

# Run the install script
RUN ./bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh --user

# Create a symlink in /usr/bin that points to /root/bazel
RUN ln -sf /root/.bazel/bin/bazel /usr/bin/