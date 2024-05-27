# Python Queryable Encryption Tutorial

This project demonstrates an example implementation of Queryable Encryption
for the PyMongo driver. To learn more about Queryable Encryption, see the
[Queryable Encryption](https://www.mongodb.com/docs/manual/core/queryable-encryption/quick-start/)
section in the Server manual.

The following sections provide instructions on how to set up and run this project.

## Install Dependencies

To run this sample app, you first need to install the following
dependencies:

- MongoDB Server version 7.0 or later
- Automatic Encryption Shared Library version 7.0 or later
- `python3`
- `pip`

For more information on installation requirements for Queryable Encryption,
see [Installation Requirements](https://www.mongodb.com/docs/manual/core/queryable-encryption/install/#std-label-qe-install).

## Configure Your Environment

1. Create a file in the root of your cloud provider's directory named `.env`.

1. Copy the contents of `env_template` into the `.env` file.

1. Replace the placeholder values in the `.env` file with your own credentials.
   For more information on setting credentials, see
   [Queryable Encryption Tutorials](https://www.mongodb.com/docs/manual/core/queryable-encryption/tutorials/)
   for KMS credentials or the
   [Quick Start](https://www.mongodb.com/docs/manual/core/queryable-encryption/quick-start/)
   for local key provider credentials.

   > **Note:** The sample application uses the `pydotenv` package to access
   > the credentials as if they were defined as environment variables, but
   > does not overwrite any environment variables you currently have set.

1. For GCP, If you downloaded your credentials in JSON format, you can use the following command to extract the value of  your private key, substituting <credentials-filename> with the name of your credentials file. The following command requires that you install OpenSSL:
    ```
    cat <credentials-filename> | jq -r .private_key | openssl pkcs8 -topk8 -nocrypt -inform PEM -outform DER | base64
    ```
    If you downloaded your credentials in PKCS12 format, you need to specify your GCP service account import password and to add a PEM pass phrase to access the key when accessing it using the following command, substituting <credentials-filename> with the name of your credentials file:
    ```
    openssl pkcs12 -info -in <credentials-filename>
    ```

## Run the Application

1. In a shell, navigate to the directory in which the application
   is saved.

1. Run `python3 -m pip install -r requirements.txt` to install the Python driver and
   `pymongocrypt`.

1. In `queryable-encryption-tutorial.py`, replace the placeholder `<Your KMS
   Provider Name>` with a valid KMS provider name.

1. Run `python3 queryable_encryption_tutorial.py` to run the application.

1. If successful, the application will print the sample document to the console.