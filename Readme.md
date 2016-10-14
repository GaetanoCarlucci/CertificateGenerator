## CertificateGenerator

This script creates self-signed SSL certificate that expires in one year. It can be used for testing purpose.

This script is based on the work that has been done for [QUIC](https://www.chromium.org/quic/playing-with-quic).


### Example: Generate a self-signed certificate for localhost server.

Modify the file ```leaf.cnf```  according to your server info. In the case of localhost be sure that these fields are correctly set:
```
CN = 127.0.0.1
.....
[other_hosts]
DNS.1 = localhost
IP.1 = 127.0.0.1
```

The run ```generate-certs.sh```:
```
./generate-certs.sh
```

This will create the dir ```out``` which contains what we need.

In particular the private key and the certificate should be added to the Web Server.

The private key of the Web server is:
```
out/leaf_cert.pkcs8
```
or this:
```
out/leaf_cert.key
```
This depends on the requirements of your server.

The certificate of the Web server is:
```
out/leaf_cert.pem
```

Finally on the client host the CA certificate has be added.

The CA certificate is:
```
out/2048-sha256-root.pem
```
and it has t obe added on the client host:
```
cp out/2048-sha256-root.pem /usr/local/share/ca-certificates/2048-sha256-root.crt
update-ca-certificates --fresh
```