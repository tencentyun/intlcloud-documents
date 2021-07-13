## Installation Issues

### setuptools is too old

Problem: `error in scf setup command: 'install_requires' must be a string or list of strings containing valid project/version requirement specifiers`

Solution: `pip install -U setuptools`

### The existing distutils installation package cannot be upgraded

Problem: ```Cannot uninstall 'PyYAML'. It is a distutils installed project and thus we cannot accurately determine which files belong to it which would lead to only a partial uninstall.```

Solution: `pip install -I PyYAML==x.x.x` (view the specific version in requirements.txt)

### six is too old
Problem: `pip "Cannot uninstall 'six'. It is a distutils installed project..."` 

Solution: `sudo pip install six --upgrade --ignore-installed six` 

### pytz is too old
Problem: ```uninstalling pytz : [error 1] Operation not permitted ...```

Solution: `sudo pip install pytz --upgrade --ignore-installed six` 



## Usage Issues

### How do I specify a function for local debugging if the YAML configuration file contains multiple function descriptions?

Problem: `Error: You must provide a function identifier (function's Logical ID in the template). Possible options in your template: ['xxxB', 'xxxA']`

Solution: include the function name when running the `local invoke` command, such as `scf local invoke -t template.yaml xxxA`

### The `[SSL: CERTIFICATE_VERIFY_FAILED]` error occurred during deployment

Problem: when `deploy` was used, function deployment failed with error message `[SSL: CERTIFICATE_VERIFY_FAILED]`

Cause: in macOS 10.12 + Python 3.6 and higher versions, Python no longer reads certificates from the system path, resulting in certificate reading failures, and SSL verification will fail when TencentCloud API is called for deployment

Solution: in the Python installation directory, run the `Install Certificates.command` script to install the `certifi` package automatically
