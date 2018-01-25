FROM openjdk:8

MAINTAINER nickersoft@gmail.com

# Add Buck dependencies
RUN apt-get update && apt-get install -y git ant gcc python python-dev

# Create a new Buck user account, creating a home directory and disabling a login shell
RUN useradd -m -s /bin/false buck

# Make a root Buck directory and give its ownership over to the buck user
RUN mkdir /buck && chown buck /buck

# Switch user to buck
USER buck

# Clone the Buck repo to /buck
RUN git clone https://github.com/facebook/buck.git /buck/

# Change the working directory to /buck
WORKDIR /buck

# Build Buck
RUN ant

# Switch back to the root user
USER root

# Create a symlink in /usr/bin that points to /buck/bin/buck
RUN ln -sf /buck/bin/buck /usr/bin/