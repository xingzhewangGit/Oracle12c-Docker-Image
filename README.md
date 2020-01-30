# Oracle12c-Docker-Image
to build the Oracle12c Docker Image

1, clone the repo of Official source for Docker configurations, images, Dockerfiles for Oracle products from https://github.com/oracle/docker-images

2, download Oracle Database 12c Release from Oracle official website
https://www.oracle.com/database/technologies/oracle-database-software-downloads.html
and save in the respective dockerfiles subdirectory, e.g. docker-images/OracleDatabase/SingleInstance/dockerfiles/12.1.0.2

3, create the image by running
# ./buildDockerImage.sh -v 12.1.0.2 -s        for standard edition of 12c release 1, or
# ./buildDockerImage.sh -v 12.2.0.1 -e        for enterprise edition of 12c release 2





Possible Exceptions you may counter 
when you see below error:
COPY failed: stat /var/lib/docker/tmp/docker-builder594691303/linuxamd64_12102_database_se2_1of2.zip: no such file or directory
please double check if you've downloaded the right installation file from Oracle website

when you see below Yum error:
https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/getPackage/gcc-4.8.5-39.0.3.el7.x86_64.rpm: [Errno 14] curl#18 - "transfer closed with 12830776 bytes remaining to read"
please add below in your docker Docker daemon configuration file daemon.json
  "dns": ["10.75.0.1", "8.8.8.8"]

10.75.0.1 here is the DNS you are using, you can replace it with your actual DNS.

to know your actual DNS, you can run below on your Mac
# dig yum.oracle.com -4
