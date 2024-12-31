# Dockerfile for SSH-enabled container
FROM ubuntu:22.04

# Build arguments for customization
ARG USERNAME=admin
ARG USER_PASSWORD=admin
ARG USER_ID=1000

# Install SSH server and other necessary packages
RUN apt-get update && \
    apt-get install -y openssh-server sudo python3 && \
    mkdir /run/sshd

# Create user with sudo privileges
RUN useradd -rm -d /home/${USERNAME} -s /bin/bash -g root -G sudo -u ${USER_ID} ${USERNAME} && \
    echo "${USERNAME}:${USER_PASSWORD}" | chpasswd && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Generate SSH host keys
RUN ssh-keygen -A

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]
