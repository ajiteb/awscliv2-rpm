# awscliv2-rpm

Automated RPM packaging of AWS CLI v2 using GitHub Actions

_Note:-_ This RPM is tested on RHEL 8 and 9, but should work on any RHEL-based distribution. The spec file is configured to install the AWS CLI in `/usr/aws-cli` and create a symlink at `/usr/bin/aws` for easy access.

# Building the RPM locally

1. `./check_for_new_installer` - download the [installer](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip) and update various metadata files
1. `./respecit` - update the spec file to match the downloaded version
1. `docker-compose build builder` - create the builder image
1. `docker-compose run builder ./rebuildit` - rebuild the RPM
1. `docker-compose run tester ./retestit` - test installing the RPM

This should result in:

- no-source RPM: `SRPMS/awscliv2-${VERSION}-${RELEASE}.nosrc.rpm`
- installable RPM: `RPMS/x86_64/awscliv2-${VERSION}-${RELEASE}.x86_64.rpm`
