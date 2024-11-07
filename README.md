# Python Queryable Encryption Tutorial

This tutorial demonstrates how to implement Queryable Encryption with the PyMongo driver. For comprehensive documentation, see the [Queryable Encryption documentation](https://www.mongodb.com/docs/manual/core/queryable-encryption/quick-start/).

## Prerequisites

The following components must be installed before running this application:

- MongoDB Server (v7.0+)
- Automatic Encryption Shared Library (v7.0+)
- Python 3
- pip

For detailed installation requirements, refer to the [Installation Guide](https://www.mongodb.com/docs/manual/core/queryable-encryption/install/#std-label-qe-install).

## Environment Setup

1. Create a `.env` file in your cloud provider's root directory:
   ```bash
   cp env_template .env
   ```

2. Update the `.env` file with your credentials. For guidance, see:
   - [Queryable Encryption Tutorials](https://www.mongodb.com/docs/manual/core/queryable-encryption/tutorials/) for KMS credentials
   - [Quick Start Guide](https://www.mongodb.com/docs/manual/core/queryable-encryption/quick-start/) for local key provider credentials

   Note: The application uses `pydotenv` to manage credentials without modifying existing environment variables.

3. For GCP users:

   **JSON Format Credentials:**
   ```bash
   cat <credentials-filename> | jq -r .private_key | openssl pkcs8 -topk8 -nocrypt -inform PEM -outform DER | base64
   ```

   **PKCS12 Format Credentials:**
   ```bash
   openssl pkcs12 -info -in <credentials-filename>
   ```
   This command requires your GCP service account import password.

## Application Setup

1. Install required packages:
   ```bash
   python3 -m pip install -r requirements.txt
   ```

2. Configure KMS provider:
   - Open `queryable-encryption-tutorial.py`
   - Replace `<Your KMS Provider Name>` with your provider's name

## Running the Application

Execute the application:
```bash
python3 queryable_encryption_tutorial.py
```

A successful run will output the sample document to the console.

## Running with Docker

You can also run the application using Docker with the provided Dockerfile in the `gcp` directory.

### Build the Docker Image

```bash
docker build -t <name> --platform linux/arm64 .
```

### Run the Container

```bash
docker run --platform linux/arm64 -a STDERR -a STDOUT \
    -e MONGODB_URI="<connection-string>" \
    -e GCP_PROJECT_ID="<project-id>" \
    -e GCP_LOCATION="<region>" \
    -e GCP_KEY_RING="<key-ring-name>" \
    -e GCP_KEY_NAME="<key-name>" \
    -e GCP_EMAIL="<service-account-email>" \
    -e GCP_PRIVATE_KEY="<private-key>" \
    <app-name>
```

Replace the placeholder values:
- `<name>`: Your desired Docker image name
- `<connection-string>`: Your MongoDB connection string
- `<project-id>`: Your GCP project ID
- `<region>`: Your GCP region
- `<key-ring-name>`: Your GCP key ring name
- `<key-name>`: Your GCP key name
- `<service-account-email>`: Your GCP service account email
- `<private-key>`: Your GCP private key
- `<app-name>`: The name you used when building the Docker image

Note: The Docker configuration is set up for ARM64 architecture. If you're using a different architecture, adjust the `--platform` flag accordingly.

## Additional Resources

- [MongoDB Queryable Encryption Documentation](https://www.mongodb.com/docs/manual/core/queryable-encryption/quick-start/)
- [Installation Requirements Guide](https://www.mongodb.com/docs/manual/core/queryable-encryption/install/#std-label-qe-install)
- [Tutorials](https://www.mongodb.com/docs/manual/core/queryable-encryption/tutorials/)