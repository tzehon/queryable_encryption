# Use Ubuntu 22.04 as base image
FROM --platform=linux/amd64 ubuntu:22.04

# Avoid timezone prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt-get update && apt-get install -y \
    wget \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements and install Python dependencies
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

# Download and install MongoDB Automatic Encryption Shared Library
RUN wget https://downloads.mongodb.com/linux/mongo_crypt_shared_v1-linux-x86_64-enterprise-ubuntu2204-7.0.2.tgz \
    && tar -xvf mongo_crypt_shared_v1-linux-x86_64-enterprise-ubuntu2204-7.0.2.tgz \
    && mkdir -p /usr/local/lib \
    && cp lib/mongo_crypt_v1.so /usr/local/lib/ \
    && rm -rf mongo_crypt_shared_v1-linux-x86_64-enterprise-ubuntu2204-7.0*

# Set environment variable for the shared library path
ENV SHARED_LIB_PATH=/usr/local/lib/mongo_crypt_v1.so

# Copy application files
COPY queryable_encryption_tutorial.py .
COPY queryable_encryption_helpers.py .

# Command to run the application
CMD ["python3", "queryable_encryption_tutorial.py"]