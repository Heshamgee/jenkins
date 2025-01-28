FROM alpine:latest

# Install required packages
RUN apk update && \
    apk add --no-cache openssh shadow && \
    rm -rf /var/cache/apk/*

# Create user 'hesham-remote' and set password
RUN adduser -D hesham-remote && \
    echo "hesham-remote:hesham" | chpasswd && \
    mkdir /home/hesham-remote/.ssh && \
    chmod 700 /home/hesham-remote/.ssh

# Copy public key to authorized_keys
COPY remote-key.pub /home/hesham-remote/.ssh/authorized_keys
RUN chown -R hesham-remote:hesham-remote /home/hesham-remote/.ssh && \
    chmod 600 /home/hesham-remote/.ssh/authorized_keys

# Generate SSH host keys
RUN ssh-keygen -A

# Expose SSH port
EXPOSE 22

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]
