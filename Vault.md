# Vault

## For vault login

### Using Username and password. (vault login -method=userpass username=[] password=[]  )
curl -gk --insecure -X PUT -H "X-Vault-Request: true" -d '{"password":"password"}' http://127.0.0.1:8200/v1/auth/support/login/username

  Here, v1 is the compulsory param for mentioning the api version.  <br />
   auth is to specify that we are attempting authentication step.  <br />
   support is the authentication method which i have created.  <br />
   login is to specify the login command. <br />
   username is actually path of the user which was also created inside the authentication method. <br />

It will return the client token which may be used further in the subsequent steps. 

### Using Approle (vault write auth/approle/login role_id="60ef4e96-da1e-62bd-0ddf-6ddd1dce0037" secret_id="fa004dd9-f8a1-02bc-f0ba-3c9feae49ab1")

URL: PUT http://127.0.0.1:8200/v1/auth/approle/login

## For storing kv (vault kv put secret/cred user=hex)

 curl --header "X-Vault-Token: root" -X POST --data '{"user": "hex"}' 'http://127.0.0.1:8200/v1/sys/internal/ui/mounts/secret/cred1'
 
 
## for fetching kv from specific path (vault kv get secret/cred)

 curl -s --header "X-Vault-Token: root" -X GET  "http://127.0.0.1:8200/v1/secret/data/cred"
 
 
 ## for fetching the list of all the secrets (vault kv list secret)
 
 curl -s --header "X-Vault-Token: root" -X GET  "http://127.0.0.1:8200/v1/secret/metadata?list=true"
 
 Metadata is actually used for fetching all the secrets. In the policy also, I have specified policy as "path "secret/+/*" {
		capabilities = ["create", "read", "update", "patch", "delete", "list"]
}"

## for creating approle (vault write auth/approle/role/jenkins token_policies="jenkin_policy")
 
 URL: PUT http://127.0.0.1:8200/v1/auth/approle/role/jenkins
 
 Here, we created an approle named as jenkin and linked it to the policy jenkin_policy.
 
 for getting the role-id --> vault read auth/approle/role/jenkins/role-id </br>
 for getting the secret-id --> vault write -f auth/approle/role/jenkins/secret-id
 
 ## Curl for updating Secret configuration

### payload.json
{
  "max_versions": 5,
  "cas_required": false,
}

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
    
 ## For listing all the auth path in the vault. 
  
  curl  -s --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" --request GET  "http://127.0.0.1:8200/v1/sys/auth" 

  ## For listing all the path in the secret. 
    
     curl  -s --header "X-Vault-Token: root" --request GET  "http://127.0.0.1:8200/v1/sys/" 
     
 ## For monitoring vault
 
      curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    'http://127.0.0.1:8200/v1/sys/monitor?log_level=debug'


## for listing policies
curl  -s --header "X-Vault-Token: root" -X GET 'http://127.0.0.1:8200/v1/sys/policies/acl?list=true'



 
|||
|vault login -method=userpass username=admin password=password| for logging with specific method and credentials|
|vault auth enable userpass|In order to enable the userpass as the authentication method.|
|vault kv get  secret/cred| for fetching the kv present in the vault in the secret engine at cred path|
|vault kv get  secret/cred| user=pass|Here, in the secret engine, a cred path will be created and, user and pass will get stored as the key-value pair|
|vault token capabilities cubbyhole/|It is for checking the capability or policy access of any specific secret engine|
|||
|||


 
     curl  -s --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" -d '{"level":"debug"}' --request GET  "http://127.0.0.1:8200/v1/sys/loggers" 
     
     curl \
    --header "X-Vault-Token: hvs.cMMyetiE6OeMtGzU87rWOBEb" \
    'http://127.0.0.1:8200/v1/sys/monitor?log_level=debug'





  curl  -s --header "X-Vault-Token: hvs.CAESIJ9F-m3FeVo0lekpvTAaJHJhPRW_gVSeM3gkdtDUdO9gGh4KHGh2cy42YXdHaFVXcVdYam9DZHpodDZ6MThpdWU" --request GET  "http://127.0.0.1:8200/v1/sys/auth" 






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


curl -s --header "X-Vault-Token: root" -X GET  "http://127.0.0.1:8200/v1/secret/data/cred"
 
 curl -s --header "X-Vault-Token: root" -d '{"username":"Passqored"}'  -X POST  "http://127.0.0.1:8200/v1/secret/data/cred" 


'{"format": "hex"}'

 curl --header "X-Vault-Token: root" -X POST --data '{"user": "hex"}' "http://127.0.0.1:8200/v1/secret/data/cred008989878789"


 

    
