Welcome to the AWS CodeStar sample web application
==================================================

This sample code helps get you started with a simple Java web application
deployed by AWS CodeDeploy and AWS CloudFormation to an Amazon EC2 server.

What's Here
-----------

This sample includes:

* README.md - this file
* appspec.yml - this file is used by AWS CodeDeploy when deploying the web
  application to EC2
* buildspec.yml - this file is used by AWS CodeBuild to build the web
  application
* pom.xml - this file is the Maven Project Object Model for the web application
* src/main - this directory contains your Java service source files
* src/test - this directory contains your Java service unit test files
* scripts/ - this directory contains scripts used by AWS CodeDeploy when
  installing and deploying your application on the Amazon EC2 instance
* template.yml - this file contains the description of AWS resources used by AWS
  CloudFormation to deploy your infrastructure
* template-configuration.json - this file contains the project ARN with placeholders used for tagging resources with the project ID

Getting Started
---------------

These directions assume you want to develop on your development environment or a Cloud9 environment, and not
from the Amazon EC2 instance itself. If you're on the Amazon EC2 instance, the
virtual environment is already set up for you, and you can start working on the
code.

To work on the sample code, you'll need to clone your project's repository to your
local computer. If you haven't, do that first. You can find instructions in the AWS CodeStar user guide at https://docs.aws.amazon.com/codestar/latest/userguide/getting-started.html#clone-repo.

1. Install maven. See https://maven.apache.org/install.html for details.

2. Install tomcat.  See https://tomcat.apache.org/tomcat-8.0-doc/setup.html for
   details.

3. Build the application.

        $ mvn -f pom.xml compile
        $ mvn -f pom.xml package

4. Copy the built application to the Tomcat webapp directory.  The actual
   location of that directory will vary depending on your platform and
   installation.

        $ cp target/ROOT.war <tomcat webapp directory>

4. Restart your tomcat server

5. Open http://127.0.0.1:8080/ in a web browser to view your application.

What Do I Do Next?
------------------

Once you have a virtual environment running, you can start making changes to
the sample Java web application. We suggest making a small change to
/src/main/webapp/WEB-INF/views/index.jsp first, so you can see how changes
pushed to your project's repository are automatically picked up by your project
pipeline and deployed to the Amazon EC2 instance. (You can watch the pipeline
progress on your project dashboard.) Once you've seen how that works, start
developing your own code, and have fun!

To run your tests locally, go to the root directory of the sample code and run the
`mvn clean compile test` command, which AWS CodeBuild also runs through your `buildspec.yml` file.

To test your new code during the release process, modify the existing tests or add tests
to the tests directory. AWS CodeBuild will run the tests during the build stage of your
project pipeline. You can find the test results in the AWS CodeBuild console.

Learn more about Maven's [Standard Directory Layout](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).

Learn more about AWS CodeBuild and how it builds and tests your application here:
https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html

Learn more about AWS CodeStar by reading the user guide. Ask questions or make
suggestions on our forum.

User Guide: http://docs.aws.amazon.com/codestar/latest/userguide/welcome.html

Forum: https://forums.aws.amazon.com/forum.jspa?forumID=248

How Do I Add Template Resources to My Project?
------------------

To add AWS resources to your project, you'll need to edit the `template.yml`
file in your project's repository. You may also need to modify permissions for
your project's worker roles. After you push the template change, AWS CodeStar
and AWS CloudFormation provision the resources for you.

See the AWS CodeStar user guide for instructions to modify your template:
https://docs.aws.amazon.com/codestar/latest/userguide/how-to-change-project.html#customize-project-template

What Should I Do Before Running My Project in Production?
------------------

AWS recommends you review the security best practices recommended by the framework
author of your selected sample application before running it in production. You
should also regularly review and apply any available patches or associated security
advisories for dependencies used within your application.

Best Practices: https://docs.aws.amazon.com/codestar/latest/userguide/best-practices.html?icmpid=docs_acs_rm_sec

## Setup CloudWatch monitor the Java Log4j logging

```
$ sudo wget http://s3.amazonaws.com/aws-cloudwatch/downloads/latest/awslogs-agent-setup.py
$ sudo chmod +x awslogs-agent-setup.py
$ sudo python ./awslogs-agent-setup.py --region=ap-southeast-2
```

Follow the wizard setup make sure all the settings are correct as below

```
[/home/ec2-user/javaapp/myapp.log]
datetime_format = %Y-%m-%d %H:%M:%S
file = /home/ec2-user/javaapp/myapp.log
buffer_duration = 5000
log_stream_name = {instance_id}
initial_position = end_of_file
log_group_name = Java_App_Logs

```