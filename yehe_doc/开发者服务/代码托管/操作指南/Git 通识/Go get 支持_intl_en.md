## Feature Overview

Golang Get utilizes a code management tool to remotely pull or update code packages and their dependencies and automatically compiles and installs them. The entire process is as simple as installing an application. The **go get** command can be used for multiple code repositories in CODING. The following is a quickstart guide.

## Getting Started

Suppose a user has a code repository called Repo A with a Git HTTPS URL: `https://e.coding.net/{team}/{project}/{repo}.git` (the curly braces are variables). Using the repository `https://e.coding.net/baulk/jackson/mux.git` as an example:

The user can configure module names using the following command.

```shell
go mod init e.coding.net/baulk/jackson/mux
```

To obtain a module using go get:

```shell
go get e.coding.net/baulk/jackson/mux
```

The modules of sub-repositories can be obtained when multiple repositories are used:

```shell
go get e.coding.net/baulk/jackson/mux/dev
```

The Git HTTPS clone URL of some repositories is: `https://e.coding.net/{team}/{project}.git`. The user can configure module names using the following command:

```shell
go mod init e.coding.net/team/project
```

To obtain a module using go get:

```shell
go get e.coding.net/team/project
```

>!Sub-modules cannot be directly obtained for such repositories. Use `e.coding.net/team/project/project` as the module name to obtain modules and their sub-modules.
