## Symptom

When you apply for an SSL certificate for domain validation and has added the corresponding operation, an error indicating a validation failure is reported after you click **View Domain Validation Status** on the certificate domain validation details page.


## Possible Causes

Click **View Domain Validation Status** and troubleshoot based on the error message.

### Using DNS validation

#### Cause 1: Specified DNS record value not detected. Please make sure you have added a specified DNS record for this domain or wait for the DNS record value to take effect
- The domain is in unresolvable status.

- The DNS record hasn’t taken effect.


#### Cause 2: Incorrect DNS record value. Check whether the record value is correct or wait for the DNS cache to update
- The host, record value, or other information in the DNS record is incorrect.

- After the information is corrected, the DNS cache hasn’t been updated.


#### Cause 3: A record value has been detected for your domain. Please wait for the certificate authority to review

The DNS cache or validation address limits CA from overseas accessing.

#### Cause 4: The certificate authority has approved your domain. Please wait for the status to change

The system has noticed the validation value but has not issued the certificate.

#### Cause 5: Too frequent operations. Please try again in 5 minutes

**View Domain Validation Status** is clicked too many times and thus limited by the CA.

>!
> 
> If a CAA record for a non-Tencent Cloud CA is configured for the domain, an SSL certificate cannot be issued for the domain properly. Before domain validation, check whether a CAA record is added for the domain and remove it if any.
> 


### Using file validation

#### Cause 1: Specified record value not detected. Please check if you have added the specified record value for this domain or wait for the certificate authority to review
- The validation file is not uploaded to the root directory of the website.

- The website validation file cannot be accessed or the path is incorrect.

- The website uses multi-level redirection.


#### Cause 2: The certificate authority has approved your domain. Please wait for the status to change

CA has approved but hasn’t updated the status.

## Solutions

### Using DNS validation


#### The DNS record hasn’t taken effect

It takes 0−72 hours for the DNS record to take effect globally. Please wait patiently.

#### The host, record value, or other information in the DNS record is incorrect

Check whether the record value on the **Validate Domain** page and that added to the DNS record is the same. If not, modify it.

#### After the information is corrected, the DNS cache hasn’t been updated

It takes 0−72 hours for a modified DNS record to take effect globally. Please wait patiently.

#### The DNS cache or validation address limits CA from overseas accessing

Please wait for the DNS cache to update, or check the website can be accessed through an overseas IP address. If not, open the website for the address.

#### The system has noticed the validation value but has not issued the certificate

The system has noticed the validation value and will issue the certificate in 15 minutes.

#### **View Domain Validation Status** is clicked too many times and thus limited by the CA

Do not repeatedly validate your domain. You can retry every 5 minutes.

### Using file validation

#### The validation file is not uploaded to the root directory of the website

Upload the validation file provided on the **Validate Domain** page to the root directory of the website.

#### The website validation file cannot be accessed or the path is incorrect

Check whether the validation file is accessible and is store in the root directory of the website so that the file content can be viewed when the website is browsed. For example, if the certificate is applied for the domain `cloud.tencent.com`, then, the validation content in the validation file fileauth.txt should be `tencxxxent`.
When you browse `cloud.tencent.com/.well-known/pki-validation/fileauth.txt` over HTTPS or HTTP, the browser displays the validation content `tencxxxent`.

#### The website uses multi-level redirection

File validation requires the website to return the status code of 200 directly and does not support redirection. Therefore, you are advised to set the website to directly return 200 first and add redirection after the domain is validated. 

#### The CA has approved the application but has not updated the status

You can wait for CA to update the status, or refresh the browser to see whether the certificate is issued.