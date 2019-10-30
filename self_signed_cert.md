# Generating a Self Signed Certificate

## Create a Root SSL Certificate

### Create a root key

Generate a RSA-2048 key and save it to the file rootCA.key.  This file is used to generate the root SSL certificate. You will be prompted for a pass phrase thar will need to be entered each time you use this key to generate a certificate.

`openssl genrsa -des3 -out rootCA.key 2048`

### Generate the certificate with the key

Running the command below will generate a key and save it to a file called rootCA.pem

`openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem`

## Trust the root SSL certificate

