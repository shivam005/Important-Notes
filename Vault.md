# Vault

## For vault login

### Using Username and password. 
curl -gk --insecure -X PUT -H "X-Vault-Request: true" -d '{"password":"password"}' http://127.0.0.1:8200/v1/auth/support/login/username

  Here, v1 is the compulsory param for mentioning the api version.  <br />
   auth is to specify that we are attempting authentication step.  <br />
   support is the authentication method which i have created.  <br />
   login is to specify the login command. <br />
   username is actually path of the user which was also created inside the authentication method. <br />

It will return the client token which may be used further in the subsequent steps. 

### Using Token



### payload.json
{
  "max_versions": 5,
  "cas_required": false,
}

## Curl for updating Secret configuration
curl \
   --insecure  --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    --request POST \
    --data @con.json \
    http://127.0.0.1:8200/v1/secret/
    
      
## Curl for creating Authentication Methods. 

### Approle

curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    --request POST \
    --data '{"type": "approle"}' \
    http://127.0.0.1:8200/v1/sys/auth/approle
    
    Here, the path parameter /approle is actually used for auto-creating the authentication method. The type parameter is actually being used in order to
    specify the type of authentication method. 
    
 ###  JWT 
    
    curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    --request POST \
    --data '{"type": "jwt"}' \
    http://127.0.0.1:8200/v1/sys/auth/jwt1
    
    
    
  ##  For generating random bit. 
  
   curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    --request POST \
    --data '{"format": "hex/base64"}' \
    http://127.0.0.1:8200/v1/sys/tools/random/164
    
    Here, the format may be either of them. 
    
 ## For listing all the path in the vault. 
  
  curl  -s --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" --request GET  "http://127.0.0.1:8200/v1/sys/auth" 

  ## For listing all the path in the secret. 
    
     curl  -s --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" --request GET  "http://127.0.0.1:8200/v1/sys/audit-hash/file" 










curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    --request LIST \
    http://127.0.0.1:8200/v1/secret/data/cred


curl -gk -H 'X-Vault-Token:hvs.cMMyetiE6OeMtGzU87rWOBEb' http://127.0.0.1:8200/v1/username/data/cred

    curl \
   --insecure  --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    -X LIST \
    http://127.0.0.1:8200/v1/secret
    
    curl \
    -H "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    -X get \
    http://127.0.0.1:8200/v1/support/data/cred/


curl -gk -H 'X-Vault-Token:hvs.cMMyetiE6OeMtGzU87rWOBEb' http://127.0.0.1:8200/v1/username/data/cred



 
 


'{"format": "hex"}'

 
    
