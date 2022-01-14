
## Official Repository
Official repository address: `https://github.com/terraform-providers/terraform-provider-tencentcloud`.


## Development Steps
1. Prepare the Go development environment. 
  The latest Go version is required, which is currently 1.14.x.
2. Register at [GitHub](https://github.com/join). 
3. [Configure two-factor authentication](https://help.github.com/en/github/authenticating-to-github/configuring-two-factor-authentication) to activate your GitHub account.  
4. Fork an official repository.  
Fork the master branch of the official repository to your account.
5. Use `git clone` to clone the repository under your account to a local path.
  Run the following command to clone.
```bash
git clone https://github.com/your-github-name/terraform-provider-tencentcloud
```
6. Complete the routine check.
Run the following command to complete the check before committing.
```bash
make hooks
```
7. Check out the branch.
Check whether the branch format is `type/module-keyword`; for example, `feat/tke-support-addon` indicates that the addon feature is added to the TKE module.
8. Modify the code. 
See [Code Style](#codeStyle) for consistency with the existing style.
9. Modify the test case.  
If there are modifications, make sure that all the test cases are accurate and passed.
10. Implement automatic document generation.
Run the following command to automate document generation. Your code must conform to certain rules as detailed in [Terraform docs generator](https://github.com/terraform-providers/terraform-provider-tencentcloud/blob/master/gendoc/README.md).
```bash
make doc
```
11. Commit the code.
Run the following command to commit the code. Make sure that the committed messages are as clear and standard as possible.
```bash
git commit  
```
12. Push the code.
Run the following command to push the code to the repository under your account.
```bash
git push
```
13. Commit the pull request.
It is not allowed to merge the code directly to the official repository without PR + code review.
14. Notify others for code review.
The code can be merged after approval by at least one member. You are not allowed to merge the code committed by yourself.
15. Release versions regularly. 
Plugins will be updated and features will take effect only after version release.

## Code Style[](id:codeStyle)

Constrain the code style as instructed in [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments):

- Variable/Function names should follow the camel case convention, with the first letter in upper or lower case depending on access control.
- A single line of code should not contain more than 120 characters.
- Add a space between operators and operands, such as `num := a + b`, except when they are used as input or array subscripts.
- Import a package using its full but not relative path.
- Put the returned value of a function error at the end.
- Return an error or null as soon as possible when necessary. Do not put an `else` after the `if` statement returns a value.
- Return the error of a function call independently without judging other conditions.
- Do not use a magic variable twice, such as region ID `9` (for Singapore); instead, use a constant, such as `const AP_SINGAPORE = 9`.


<dx-alert infotype="notice" title="">
You can format code with the `make fmt` command. You must run `make hooks` containing a formatting step mentioned in the development steps.
</dx-alert>




## Version/Tag Rule
Version names should follow the principles of [Semver](https://semver.org/) and be prefixed with `v`, such as `v1.2.3`.

## CHANGELOG.md Rule
You must update `CHANGELOG.md` upon every modification according to the following versioning rules:

- **FEATURES**: when you add a data source or resource.
- **ENHANCEMENTS**: when you update a data source or resource.
- **BUG FIXES**: when you fix a bug.
- **DEPRECATED**: when you deprecate a data source, resource, or field.

According to the Semver master/sub/patch rules above, release a 1.X.0 subversion for FEATURES and DEPRECATED, and release a 1.0.X patch for ENHANCEMENTS and BUG FIXES.

## Dynamic Input Limit
When users access Tencent Cloud services, you often need to limit the input arguments. For example, you need to limit the selectable database versions when a user purchases a TencentDB for PostgreSQL instance. As the list of supported database versions is updated from time to time, without a timely update, the user may not be able to select the latest version, preventing normal use of the service. In this case, the list should not be specified directly in the code; instead, it should be dynamically pulled through an API.

This principle also applies to versions and memory specifications supported by TencentDB for PostgreSQL and TencentDB for Redis as well as programming languages and versions supported by SCF.
