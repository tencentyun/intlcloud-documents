## Hosting and Protecting Secrets
**Example**: DB admin can create a secret (MySecret) and specify the version (MyVersion1). The database username and password are encrypted and stored using SSM. If no KMS key is specified, SSM will automatically create a default key.
```
var (
    secretName = "MySecret1"
    version = "MyVersion1"
    plainText = "user:password@tcp(127.0.0.1:3306)/test"
)

func ExampleCreateSecret() {
    credential := common.NewCredential(
       secretId,
       secretKey,
     )
    cpf := profile.NewClientProfile()
    cpf.HttpProfile.Endpoint = endpoint
    client, _ := ssm.NewClient(credential, region, cpf)

    request := ssm.NewCreateSecretRequest()
    request.SecretName = &secretName
    request.VersionId = &version
    request.SecretString = &plainText

    resp, err := client.CreateSecret(request)
    if err != nil {
       // error handler
    }
    fmt.Println(*resp.Response.SecretName)

     // create ok
}
```

## Viewing the Metadata of Secrets
- **Example 1**: Obtaining the secret list and metadata of secrets.
```
func ExampleListSecrets() {
      credential := common.NewCredential(
          secretId,
          secretKey,
      )
      cpf := profile.NewClientProfile()
      cpf.HttpProfile.Endpoint = endpoint
      client, _ := ssm.NewClient(credential, region, cpf)
		
      request := ssm.NewListSecretsRequest()
		
      resp, err := client.ListSecrets(request)
      if err != nil {
        // error handler
      }
      fmt.Println(resp.Response.SecretMetadatas)
       // get secrets metadata
       // ...
}
```

- **Example 2**: Obtaining the version information using the secret name (MySecret1)
```
var (
       secretName = "MySecret1"
)
  func ExampleListSecretVersionIds() {
      credential := common.NewCredential(
          secretId,
          secretKey,
      )
      cpf := profile.NewClientProfile()
      cpf.HttpProfile.Endpoint = endpoint
      client, _ := ssm.NewClient(credential, region, cpf)
		
      request := ssm.NewListSecretVersionIdsRequest()
      request.SecretName = &secretName
		
      resp, err := client.ListSecretVersionIds(request)
      if err != nil {
         // error handler
      }
      fmt.Println(resp.Response.Versions)
		
      // get version list
      // ...
}
```

## Obtaining the Sensitive Data Plaintext Stored in SSM.
**Example**: The caller obtains the database username and password plaintext using the secret name (MySecret1) and secret version (MyVersion1).
```
var (
    secretName = "MySecret1"
    version = "MyVersion1"
 )

func ExampleGetSecretValue() {
    credential := common.NewCredential(
        secretId,
        secretKey,
    )
    cpf := profile.NewClientProfile()
    cpf.HttpProfile.Endpoint = endpoint
    client, _ := ssm.NewClient(credential, region, cpf)

    request := ssm.NewGetSecretValueRequest()
    request.VersionId = &version
    request.SecretName = &secretName

    resp, err := client.GetSecretValue(request)
    if err != nil {
        // error handler
    }
    fmt.Println(*resp.Response.SecretString)

    // get plain text, connect db
    // ...
}
```

## Updating the Content of a Secret
**Example**: Updating the database username and password plaintext using the secret name (MySecret1) and version (MyVersion1).
```
var (
    secretName = "MySecret1"
    version = "MyVersion1"
    newSecretValue = "user2:password2@tcp(127.0.0.1:3306)/test"
)

func ExamplePutSecretValue() {
    credential := common.NewCredential(
        secretId,
        secretKey,
    )
    cpf := profile.NewClientProfile()
    cpf.HttpProfile.Endpoint = endpoint
    client, _ := ssm.NewClient(credential, region, cpf)

    request := ssm.NewPutSecretValueRequest()
    request.SecretName = &secretName
    request.VersionId = &version
    request.SecretString = &newSecretValue

    resp, err := client.PutSecretValue(request)
    if err != nil {
        // error handler
    }
    fmt.Println(*resp.Response.SecretName)
    // secret updated
    // ...
}
```

## Disabling, Deleting, and Restoring a Secret
- **Example 1**: Disabling a secret. After a secret is disabled, the server can no longer obtain any content of the secret.
```
var (
      secretName = "MySecret1"
)
func ExampleDisableSecret() {
      credential := common.NewCredential(
           secretId,
           secretKey,
      )
      cpf := profile.NewClientProfile()
      cpf.HttpProfile.Endpoint = endpoint
      client, _ := ssm.NewClient(credential, region, cpf)
		
      request := ssm.NewDisableSecretRequest()
      request.SecretName = &secretName
      resp, err := client.DisableSecret(request)

      if err != nil {
         // error handler
      }
      fmt.Println(*resp.Response.SecretName)
      // secret disabled
      // ...
}
```
- **Example 2**: Deleting a secret. You can set the schedule delete time, before which the secret can be restored.
>!Only disabled secrets can be deleted.
>
```
func ExampleDeleteSecret() {
      credential := common.NewCredential(
           secretId,
           secretKey,
      )
      cpf := profile.NewClientProfile()
      cpf.HttpProfile.Endpoint = endpoint
      client, _ := ssm.NewClient(credential, region, cpf)
		
      request := ssm.NewDeleteSecretRequest()
      request.SecretName = &secretName
      request.RecoveryWindowInDays = &recoverWindowsInDays
		
      resp, err := client.DeleteSecret(request)
      if err != nil {
        // error handler
      }
      fmt.Println(*resp.Response.DeleteTime)
      // secret deleted
      // ...
}
```

- **Example 3**: Restoring a secret. You can restore and enable the `PendingDelete` secret.
```
func ExampleRestoreSecret() {
      credential := common.NewCredential(
          secretId,
          secretKey,
      )
      cpf := profile.NewClientProfile()
      cpf.HttpProfile.Endpoint = endpoint
      client, _ := ssm.NewClient(credential, region, cpf)
		
      request := ssm.NewRestoreSecretRequest()
      request.SecretName = &secretName
		
      resp, err := client.RestoreSecret(request)
      if err != nil {
           // error handler
      }
      fmt.Println(*resp.Response.SecretName)
      // secret restored
      // ...
}
```
