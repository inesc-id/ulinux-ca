# uLinux CA skeleton

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
    openssl req -config openssl.cnf -key private/server.key.pem -new -sha256 -out newcerts/server.key.pem

    # sign certificate request with ca
    openssl ca -config openssl.cnf -extensions server_cert -days 375 -notext -md sha256 -in newcerts/server.csr.pem -out certs/server.crt.pem
