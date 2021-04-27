## setup
```
vault write -force transit/keys/rsa-4096 type=rsa-4096
```

```console
vault read transit/keys/rsa-4096
Key                       Value
---                       -----
allow_plaintext_backup    false
deletion_allowed          false
derived                   false
exportable                false
keys                      map[1:map[creation_time:2021-04-27T15:34:07.43088+09:00 name:rsa-4096 public_key:-----BEGIN PUBLIC KEY-----
xxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxx
-----END PUBLIC KEY-----
]]
latest_version            1
min_available_version     0
min_decryption_version    1
min_encryption_version    0
name                      rsa-4096
supports_decryption       true
supports_derivation       false
supports_encryption       true
supports_signing          true
type                      rsa-4096
```

## sign data
```console
vault write transit/sign/rsa-4096/sha2-512 input=dGVzdA==
Key            Value
---            -----
key_version    1
signature      vault:v1:xxxxxxx
```

```console
vault write transit/verify/rsa-4096/sha2-512 input=dGVzdA== signature=${SIG}
Key      Value
---      -----
valid    true
```

```console
vault write transit/verify/rsa-4096/sha2-512 input=dGVzdHRlc3Q= signature=${SIG}
Key      Value
---      -----
valid    false
```

## hmac
```console
vault write transit/hmac/rsa-4096/sha2-512 input=dGVzdA==
Key     Value
---     -----
hmac    vault:v1:xxxxxxx
```

```console
vault write transit/verify/rsa-4096/sha2-512 input=dGVzdA== hmac=${HMAC}
Key      Value
---      -----
valid    true
```

```console
vault write transit/verify/rsa-4096/sha2-512 input=dGVzdHRlc3Q= hmac=${HMAC}
Key      Value
---      -----
valid    false
```