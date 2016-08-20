# EPICS V4 Jenkins Jobs

The templates and definitions in this repository are used to create
the Jenkins jobs for the EPICS V4 Continuous Integration system instance
hosted on [CloudBees](https://openepics.ci.cloudbees.com).

## Jenkins Job Builder

The tool used to create the XML job definitions is called
[Jenkins Job Builder](http://docs.openstack.org/infra/jenkins-job-builder/).

It takes simple descriptions of Jenkins jobs in YAML or JSON format
and uses them to create the XML files that configure Jenkins.

These XML job descriptions are uploaded to Jenkins using its web service API
(via https).

## How-To

### Prepare

1. Install Jenkins Job Builder (JJB).

    $ sudo pip install jenkins-job-builder

2. Clone this repository.

3. Add your CloudBees credentials to the JJB configuration file `cloudbees.ini`.
It should be possible to use an API token, but that seems not to be working
on the CloudBees Jenkins instance.

### Test

To check the generated XML, use JJB's `test` command:

    $ jenkins-jobs --conf ./cloudbees.ini test templates:cloudbees

You can add job names as additional arguments to limit the XML generation
to the specified jobs. Wildcards in job names are supported.

You can add `-o <outputdir>` to create all jobs as separate XML files.

### Update

To update the jobs on CloudBees, use JJB's `update` command:

    $ jenkins-jobs --conf ./cloudbees.ini update templates:cloudbees

Job names as additional arguments will update only the specified jobs.
Wildcards in job names are supported.

### Be Careful

JJB offers commands to delete jobs (even all jobs) on Jenkins.

**Do not use these commands.**

They will affect *all* jobs on the Jenkins instance, including those not
generated by JJB and those of other projects.
