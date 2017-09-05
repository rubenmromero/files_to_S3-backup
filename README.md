# Files-S3-Backup

Tool to do backup of directories and files on a server and send to S3 service the resulting TAR file.

## Prerequisites

* Pip tool for Python packages management. Installation:

      $ curl -O https://bootstrap.pypa.io/get-pip.py
      $ sudo python get-pip.py

* AWS IAM EC2 Role (only for executions from EC2 instances) or IAM User with the following associated IAM policy:

      Policy Name : AmazonS3FullAccess

      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
          }
        ]
      }

* AWS CLI for ec2 commands. Installation and configuration:

      $ sudo pip install awscli

      $ aws configure
      AWS Access Key ID [None]: <access_key>		# Leave blank in EC2 instances with associated IAM Role
      AWS Secret Access Key [None]: <secret_key>	# Leave blank in EC2 instances with associated IAM Role
      Default region name [None]: eu-west-1
      Default output format [None]:

## Configuration

1. Download the project code in your favourite path:

       $ git clone https://github.com/rubenmromero/files-s3-backup.git

2. Create a copy of [fs3backup.conf.dist](conf/fs3backup.conf.dist) template named `conf/fs3backup.conf` and set the backup properties with the appropiate values:

       # From the project root folder
       $ cp conf/fs3backup.conf.dist conf/fs3backup.conf
       $ vi conf/fs3backup.conf

3. If you want to schedule the periodic tool execution, copy the [files-s3-backup](cron.d/files-s3-backup) template to the `/etc/cron.d` directory and replace the existing `<tags>` with the appropiate values:

       # From the project root folder
       $ sudo cp cron.d/files-s3-backup /etc/cron.d
       $ sudo vi cron.d/files-s3-backup

## Execution Method

Once configured the backup properties into `conf/fs3backup.conf` file, simply run `bin/fs3backup.sh` script as follows:

    # ./bin/fs3backup.sh

## Related Links

* [Install the AWS CLI Using Pip](http://docs.aws.amazon.com/cli/latest/userguide/installing.html#install-with-pip)
* [Configuring the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
