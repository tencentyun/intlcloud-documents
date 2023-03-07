The provider requires continuous improvements and iteration. You can contribute your code to the repository in line with the minimal change principle, that is, implement only one enhancement or bug fix in each pull request to avoid large-scale or cross-feature code changes that can increase the test and review costs per time.

## Checking the Code

Your merge request will trigger GitHub actions related to merge check, such as formatting, documentation generation, and acceptance test. When these checks are passed, we will review your code and give our feedback or directly merge it. Before the branch is pushed to the remote, you can execute these steps locally.

### Setting the commit hook

Run `make hooks` in the directory of the local repository to install the dependencies of the formatting check and add `pre-commit.sh` to the commit hook.

### Formatting the code

Run `make fmt` to format the `go` code and import order.

### Syncing the documentation

Run `make doc`. Then, the `./gendoc` script will parse and sync any change you made to `./website`.

## Writing an Acceptance Test

To ensure that your changes can work properly, you need to write acceptance test cases or add parameter assertions to existing cases to cover your changes. For detailed directions, see [Writing Test Case](https://www.tencentcloud.com/document/product/1172/52381). Testing paid resources will initiate the actual billing process. Or you can write test cases and have them executed by us.

