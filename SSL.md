# SSL

### Generate a self-signed certificate. You can use the Java keytool utility to generate a self-signed certificate.
keytool -genkeypair -alias localhost -keyalg RSA -keystore localhost.jks

### By default, Java does not trust self-signed certificates. To trust the self-signed certificate, you need to add it to the Java trust store. To do this, run the following command:
openssl req -x509 -newkey rsa:2048 -nodes -keyout localhost.key -out localhost.crt -subj="/C=US/CN=localhost"
### First
keytool -importcert -alias localhost -file localhost.crt -keystore cacerts
### 
Below is the way to import multiple certs in the truststore, It is done using alias.
keytool -import -file C:\cascerts\firstCA.cert -alias firstCA -keystore myTrustStore




1) trust store creation using pem file

keytool -import -v -trustcacerts -alias endeca-ca -file cacert-0-0.pem -keystore ru_truststore.jks  -deststoretype jks

2) keystore creation 

i) create pkc12  using  .key and server.pem and all CA pem

openssl pkcs12 -inkey key-x-x.pem -in cert-0-0.pem -export -out ru_keystore.p12

ii)  using pkc12 create keystore jsk

keytool -importkeystore -srckeystore  ru_keystore.p12  -srcstoretype pkcs12 -destkeystore  ru_keystore.jks -deststoretype jks



keytool -importkeystore -srckeystore ru_keystore.jks -destkeystore ru_keystore.jks -deststoretype pkcs12



>>>>> To check private key and cert are same or not, it will return same value if crt and prvt are same
openssl rsa -modulus -noout -in <private key file>
openssl x509 -modulus -noout -in <certificate file>


>>>>to see content of pem file
openssl x509 -in cacert-0-0.pem -text -noout

>>>>to see content of truststore file.
keytool -list -v -keystore ru_truststore.jks -storepass changeit




................................................
## Generate CSR
### Generate private key
openssl ecparam -name prime256v1 -genkey -noout -out private-key.pem
### Generate CSR
openssl req -out CSR.csr -key private-key.pem -new 
### To list all the curves in the ec cryptography 
openssl ecparam -list_curves

## Some General Commands 
### Check a Certificate Signing Request (CSR)
openssl req -text -noout -verify -in CSR.csr
### Check a private key
openssl rsa -in privateKey.key -check
### Check a certificate
openssl x509 -in certificate.crt -text -noout
