# to build Oracle12c-Docker-Image
to build the Oracle12c Docker Image

1, clone the repo of Official source for Docker configurations, images, Dockerfiles for Oracle products from https://github.com/oracle/docker-images

2, download Oracle Database 12c Release from Oracle official website
https://www.oracle.com/database/technologies/oracle-database-software-downloads.html
and save in the respective dockerfiles subdirectory, e.g. docker-images/OracleDatabase/SingleInstance/dockerfiles/12.1.0.2

3, create the image by running
>_ ./buildDockerImage.sh -v 12.1.0.2 -s        for standard edition of 12c release 1

or
>_ ./buildDockerImage.sh -v 12.2.0.1 -e        for enterprise edition of 12c release 2

or
>_ ./buildDockerImage.sh -v 18.4.0 -x 

4, finally you will see
Successfully built 7f9b9a83626d
Successfully tagged oracle/database:12.1.0.2-se2
  Oracle Database Docker Image for 'se2' version 12.1.0.2 is ready to be extended:     
    --> oracle/database:12.1.0.2-se2

# Possible Exceptions you may counter 
when you see below error:
COPY failed: stat /var/lib/docker/tmp/docker-builder594691303/linuxamd64_12102_database_se2_1of2.zip: no such file or directory
please double check if you've downloaded the right installation file from Oracle website

when you see below Yum error:
https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/getPackage/gcc-4.8.5-39.0.3.el7.x86_64.rpm: [Errno 14] curl#18 - "transfer closed with 12830776 bytes remaining to read"
please add below in your docker Docker daemon configuration file daemon.json
  "dns": ["10.75.0.1", "8.8.8.8"]

10.75.0.1 here is the DNS you are using, you can replace it with your actual DNS.

to know your actual DNS, you can run below on your Mac
>_ dig yum.oracle.com -4
or 
>_ docker run busybox nslookup github.com

# to run it 
>_ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
oracle/database     18.4.0-xe           b7d3a210c3a0        23 minutes ago      319MB

Docker run -d -it --name oracle18 -p 1599:1521 -p 5530:5500 -v /Users/jameswang/oradata:/opt/oracle/oradata oracle/database:18.4.0-xe



reference:
https://sqlmaria.com/2017/04/27/oracle-database-12c-now-available-on-docker/
https://development.robinwinslow.uk/2016/06/23/fix-docker-networking-dns/#the-permanent-system-wide-fix





Maven Install ojdbc8-12.2.0.1.jar

mvn install:install-file -Dfile=ojdbc8-12.2.0.1.jar -DgroupId=com.oracle.jdbc -DartifactId=ojdbc8 -Dversion=12.2.0 -Dpackaging=jar
