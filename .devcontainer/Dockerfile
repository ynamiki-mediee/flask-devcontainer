# Use Python 3.9 slim image as base
FROM python:3.9-slim

# Set environment variable to disable interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install necessary packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    libssl-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set working directory to /workspace
WORKDIR /workspace

# Copy requirements file to container
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy ssh key
# Make it possible to use git from remote container
RUN mkdir -p ~/.ssh && ln -s /run/secrets/host_ssh_key ~/.ssh/id_rsa
RUN echo 'eval `ssh-agent`' >> ~/.bashrc
RUN echo 'ssh-add ~/.ssh/id_rsa' >> ~/.bashrc

# Set default command to bash
CMD ["bash"]
