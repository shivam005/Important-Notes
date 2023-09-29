# SSL

### Generate a self-signed certificate. You can use the Java keytool utility to generate a self-signed certificate.
keytool -genkeypair -alias localhost -keyalg RSA -keystore localhost.jks

### By default, Java does not trust self-signed certificates. To trust the self-signed certificate, you need to add it to the Java trust store. To do this, run the following command:
openssl req -x509 -newkey rsa:2048 -nodes -keyout localhost.key -out localhost.crt -subj="/C=US/CN=localhost"
keytool -importcert -alias localhost -file localhost.crt -keystore cacerts


### 
