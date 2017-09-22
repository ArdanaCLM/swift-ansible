# swift-ansible Ardana CI environment

The project environment is run automatically as a ci job when submitting a
swift-ansible patch. See the zuul job ardana-project-stack-test.

There are a number of other environments defined. These are used solely by
the developer i.e. they are not used by any CI job. The environment names
describe the general configuration. For example:

* cp1-keystone-swift
* cp1-keystone-swift-cp2-glance
* cp1-keystone-cp2-swift-cp3-glance
* cp1-keystone-cp2-swift-cp3-swift-cp4-glance

Use astack to build and deploy these environments. For example:

    cp ardana-dev-tools

    # Always good practice to cleanup your vagrant environment
    bin/cleanup-slave

    #  To build and deploy cp1-keystone-swift-cp2-glance:
    bin/astack.sh --project-stack ardana/swift-ansible cp1-keystone-swift-cp2-glance

    # If you don't need to re-build the venvs:
    bin/astack.sh --no-setup --no-build --project-stack ardana/swift-ansible cp1-keystone-swift-cp2-glance

Here are some useful astack command line options:

    --no-setup  Don't run dev-env-install.yml
    --no-build  Don't build venv, reuse existing packages
    --no-config Do not execute the config-processor
    --no-site   Do not execute the site.yml playbook during

To run the test plan:

    cd ardana-dev-tools/ardana-vagrant-models/project-vagrant
    ../../bin/test-project-stack.sh ardana/swift-ansible cp1-keystone-swift-cp2-glance

Note, the test plan is can be run against any environment, but it is designed
for running against the project environment.
