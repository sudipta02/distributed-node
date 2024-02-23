C:\Users\Sudipta.saho\Downloads\openssl-0.9.8k_X64\bin\openssl.exe req -nodes -new -x509 -keyout recipe-api\tls\basic-private-key.key -out shared\tls\basic-certificate.cert
 -config C:\Users\Sudipta.saho\Downloads\openssl-0.9.8k_X64\openssl.cnf
 --------This command creates two files, namely basic-private-key.key (the private key) and basic-certificate.cert (the public key).----------

 # Happens once for the CA
$ openssl genrsa -des3 -out ca-private-key.key 2048 --private key generated from this cmd (pass phrase = qwertyuiopasdfghjklzxcvbnm)
$ openssl req -x509 -new -nodes -key ca-private-key.key \ --CA(Certificate Authority) certificate is generated from the private key
  -sha256 -days 365 -out shared/tls/ca-certificate.cert \
  -config C:\Users\Sudipta.saho\Downloads\openssl-0.9.8k_X64\openssl.cnf

# Happens for each new certificate
$ openssl genrsa -out recipe-api/tls/producer-private-key.key 2048 
$ openssl req -new -key recipe-api/tls/producer-private-key.key \
  -out recipe-api/tls/producer.csr 
$ openssl x509 -req -in recipe-api/tls/producer.csr \
  -CA shared/tls/ca-certificate.cert \
  -CAkey ca-private-key.key -CAcreateserial \
  -out shared/tls/producer-certificate.cert -days 365 -sha256 

Use different common name