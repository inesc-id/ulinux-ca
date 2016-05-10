# uLinux CA skeleton

## Preparations
Create required files in `ca/`

    touch index.txt
    echo 1000 > serial

Make sure all your permissions are secure (not readable by any other potential users on the system).

## Create Root CA
    # in ca/
    # generate key
    openssl genrsa -out private/ca.key.pem 4096
    # generate certificate
    openssl req -config openssl.cnf -key private/ca.key.pem -new -x509 -days 7300 -sha256 -extensions v3_ca -out certs/ca.cert.pem

## Create certificates
    # in ca/
    # generate key
    openssl genrsa -out private/server.key.pem 2048

    # generate certificate request
    openssl req -config openssl.cnf -key private/server.key.pem -new -sha256 -out newcerts/server.csr.pem

    # sign server certificate request with ca
    openssl ca -config openssl.cnf -extensions server_cert -days 375 -notext -md sha256 -in newcerts/server.csr.pem -out certs/server.crt.pem

    # sign client certificate request with ca
    openssl ca -config openssl.cnf -extensions usr_cert -days 375 -notext -md sha256 -in newcerts/client1.csr.pem -out certs/client1.crt.pem
