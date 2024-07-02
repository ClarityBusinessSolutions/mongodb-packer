# MongoDB Packer

This repository contains tuned packer images that create AWS AMI's for
the [MongoDB Ops Manager](https://www.mongodb.com/docs/ops-manager/current/), [AppDB](https://www.mongodb.com/docs/ops-manager/current/tutorial/prepare-backing-mongodb-instances/), and the [MongoDB Agent](https://www.mongodb.com/docs/ops-manager/current/tutorial/nav/mongodb-agent/).

Images use RedHat Enterprise Linux 8.

## Building the Images

To build the images, you will need to have the [AWS CLI](https://aws.amazon.com/cli/) installed, be able to connect to AWS from the terminal running the packer scripts, and have [HashiCorp Packer](https://www.packer.io) installed.

### Building the AppDB

```shell
cd app-db
export AWS_MAX_ATTEMPTS=60 AWS_POLL_DELAY_SECONDS=60
packer build -timestamp-ui .
```

### Building the Ops Manager

```shell
cd ops-manager
export AWS_MAX_ATTEMPTS=60 AWS_POLL_DELAY_SECONDS=60
packer build -timestamp-ui .
```

### Building the MongoDB Agent

```shell
cd mongodb-agent
export AWS_MAX_ATTEMPTS=60 AWS_POLL_DELAY_SECONDS=60
packer build -timestamp-ui .
```

## Customizing the Images

Each of the images contains a `variables.pkr.hcl` file which allows users to customize the scripts to meet the requirements of their environment.

### AppDB Customization

The following table contains a description of the variables in the AppDB's [variables.pkr.hcl](./app-db/variables.pkr.hcl) file.

| Variable | Description | Default Value |
|----------|----------|----------|
| mongodb_major_version | The major version of MongoDB Database to install. See [MongoDB Releases](https://www.mongodb.com/try/download/enterprise-advanced/releases) for all current releases and [Archived Releases](https://www.mongodb.com/try/download/enterprise-advanced/releases/archive) for all archived rleases. | 6.0 |
| mongodb_patch_version | The patch release of MongoDB to install | 8 |
| db_tools_version | The version of MongoDB tools to install | 100.7.5 |
| source_ami_name | Glob that will be used to search for the source AMI Name. The most recent match will be used | RHEL-8*_HVM-*-x86_64-*-Hourly2-GP2 |
| source_ami_owner | AWS account ID that owns the source AMI. The default is the account ID for certified RedHat images. | 309956199498 |
| instance_type | The AWS instance type to use to build the AppDB Instances. | m5.large |
| region | The AWS region to use for the AppDB Instances. | us-east-1 |

### Ops Manager Customization

The following table contains a description of the variables in the AppDB's [variables.pkr.hcl](./ops-manager/variables.pkr.hcl) file.

| Variable | Description | Default Value |
|----------|----------|----------|
| ops_manager_version | The version of MongoDB Ops Manager to install.  See [Ops Manager Versions](https://www.mongodb.com/try/download/ops-manager) for all available versions. | 7.0.8 |
| source_ami_name | Glob that will be used to search for the source AMI Name. The most recent match will be used | RHEL-8*_HVM-*-x86_64-*-Hourly2-GP2 |
| source_ami_owner | AWS account ID that owns the source AMI. The default is the account ID for certified RedHat images. | 309956199498 |
| instance_type | The AWS instance type to use to build the AppDB Instances. | m5.large |
| region | The AWS region to use for the AppDB Instances. | us-east-1 |

### MongoDB Agent

The following table contains a description of the variables in the AppDB's [variables.pkr.hcl](./app-db/variables.pkr.hcl) file.

| Variable | Description | Default Value |
|----------|----------|----------|
| mongodb_major_version | The major version of MongoDB Database to install. See [MongoDB Releases](https://www.mongodb.com/try/download/enterprise-advanced/releases) for all current releases and [Archived Releases](https://www.mongodb.com/try/download/enterprise-advanced/releases/archive) for all archived rleases. | 6.0 |
| mongodb_patch_version | The patch release of MongoDB to install | 8 |
| db_tools_version | The version of MongoDB tools to install | 100.7.5 |
| source_ami_name | Glob that will be used to search for the source AMI Name. The most recent match will be used | RHEL-8*_HVM-*-x86_64-*-Hourly2-GP2 |
| source_ami_owner | AWS account ID that owns the source AMI. The default is the account ID for certified RedHat images. | 309956199498 |
| instance_type | The AWS instance type to use to build the AppDB Instances. | m5.large |
| region | The AWS region to use for the AppDB Instances. | us-east-1 |

