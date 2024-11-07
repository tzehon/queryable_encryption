FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y python3-pip && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

RUN mkdir -p /usr/local/lib
COPY mongo_crypt_shared_v1-linux-aarch64-enterprise-ubuntu2204-8.0.3/lib/mongo_crypt_v1.so /usr/local/lib/

ENV SHARED_LIB_PATH=/usr/local/lib/mongo_crypt_v1.so

COPY queryable_encryption_tutorial.py .
COPY queryable_encryption_helpers.py .

CMD echo "Starting application..." && \
    python3 -u queryable_encryption_tutorial.py || \
    (echo "Application failed with exit code $?" && exit 1)