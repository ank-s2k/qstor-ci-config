# Qstor project-config repository

This is a fork of project-config repository for use as a
starting point to setup our 3rd party CI account. It is expected that you
fork this repository or otherwise copy it to your own repository. Any
changes to this version are expected to remain within the scope of an
'example' to help others get started. Refer to
[openstack-infra/project-config](https://git.openstack.org/cgit/openstack-infra/project-config/)
for a more complete production configuration.

# Steps to begin customization

The project-config repository is intended to contain custom configurations
needed by each CI system.

## Customize Zuul

The zuul layout configuration is located in `zuul/layout.yaml`. You can find
the full configuration details in the [Zuul manual](http://docs.openstack.org/infra/zuul/).

1. Change 'myvendor' in the 'recheck' command to your CI's name.

2. Configure the e-mail addresses for merge-failures and job notification.

3. By default, the project zuul triggers on is `openstack-dev/ci-sandbox`.
   After testing your CI system update this section to include other projects.
   You are encouraged to use the 'silent' pipeline until your jobs are stable.

## Customize Nodepool

The nodepool configuration is located in `nodepool/nodepool.yaml`. You can
find the full configuration instructions in the [Nodepool manual](http://docs.openstack.org/infra/nodepool/).
There are a few configuration that need to be updated.

1. There are some user names and passwords that need to be configured.

2. Select a 'random time' for your nodepool images to be built in the
   `image-update` property. By having 3rd party systems use different
   times will help reduce the spike load on OpenStack's Git servers.

3. Setup an intial set of nodepool scripts and elements. Start by cloning
   OpenStack's [project-config](https://git.openstack.org/cgit/openstack-infra/project-config/)
   and copying the entire contents of that repo's `nodepool/elements` to your repo's
   `nodepool/elements`. Optionally do the same for the `nodepool/scripts`
   folder. You may have to change these elements to work in your environment.
   If so, see this [README](http://git.openstack.org/cgit/openstack-infra/project-config/tree/nodepool/elements/README.rst)
   for help.

4. Update the nodepool/nodepool.yaml `diskimages` configuration to
   match the elements you included in the previous step. If you included everything, the defaults
   provide a good starting point. Otherwise, adjust them as needed as explained
   in the [nodepool manual](http://docs.openstack.org/infra/nodepool/configuration.html#diskimages).

## Customize Jenkins Jobs

Adjust the jenkins jobs in `jenkins/jobs/` to your needs. You can find the full configuration details in the
[Jenkins Job Builder manual](http://docs.openstack.org/infra/jenkins-job-builder/)

1. Change the value of the `<your-log-server>` in project-config-example/jenkins/jobs/macros-common.yaml
   to the host you will publish
   job artifacts to. This is also known as the Log server. You can set one up using
   [openstackci::logserver puppet class](https://git.openstack.org/cgit/openstack-infra/puppet-openstackci/tree/manifests/logserver.pp)

## Basic checks

Prerequisites: The following packages need to be installed for the `zuul` tox environment tests to pass:
sudo apt-get install libxml2-dev libxslt1-dev  python-dev build-essential

1. Run `tox` to run some basic syntax checks to validate the syntax of your configuration files.

## Credits

This repository is based on work created from the following sources:

1. [openstack-infra/project-config](https://git.openstack.org/cgit/openstack-infra/project-config/)

2. [rasselin/os-ext-testing-data](https://github.com/rasselin/os-ext-testing-data)

3. [jaypipes/os-ext-testing-data](https://github.com/jaypipes/os-ext-testing-data)

