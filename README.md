# Standard Application Project Layout

## Overview

This is a basic layout for applications projects deployed in the juanah.cloud network.

## Application directory

Each application or service needs a folder matching it's name. The application folder must be alpha-numeric including "-", and must start with a letter.

### Root application directory

The root of the directory must contain atleast the following files:

- main.tf
- variables.tf
- outputs.tf
- README.md
- application.yml

#### What should not be in the root application directory

The intetion behind the application mono-repo is to deploy applications to various infrastructure locations. Therefore, only code neccessary to deploy the application should exist in this repo. Applications or services should exist in a seperate versioned repo.

#### `<app-dir>/application.yml`

The application.yml file contains enviromental specefic versions and build variables and must follow the following format:

```yml
---
<environment>:
    version: <string>
    tfvars: <string>
    variables:
        <key>:<value>
```

##### environment

The following environments are supported for CI/CD:

- `tst`
- `staging`
- `production`

##### tfvars

tfvars key contains the name of the var file for that environment located in the `env` folder.

##### variables

The application.yml file can and should include multiple enviroments. However you can seperate environments by prepending the environment like `tst.application.yml`. In this format, environment will be assumed to the tst and will be ignored if included yml file.
