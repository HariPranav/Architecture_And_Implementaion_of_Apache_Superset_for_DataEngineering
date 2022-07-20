# Architecture_And_Implementaion_of_Apache_Superset_for_DataEngineering

![image](https://user-images.githubusercontent.com/28874545/180044681-1d8b003f-a52a-4e8a-8c90-99b8cbfec5a7.png)

# Apache Superset A Visualization Tool

'Apache Superset is a modern data exploration and visualization platform. Superset is fast, lightweight, intuitive and loaded with options that make it easy for users of all skill sets to explore and visualize the data. It can handle simple charts to highly detailed geospatial charts'

Apache Superset is a an open source visualization tool which provides out of the box integrations with a wide variety of databases and cloud platfroms. It can be easily deployed on EC2 machines and has great features which meet the production grade requirements like

1. POWERFUL YET EASY TO USE

Quickly and easily integrate and explore your data, using either our simple no-code viz builder or state of the art SQL IDE.

2. INTEGRATES WITH MODERN DATABASES

Superset can connect to any SQL based data source through SQLAlchemy, including modern cloud native databases and engines at petabyte scale.

3. MODERN ARCHITECTURE

Superset is lightweight and highly scalable, leveraging the power of your existing data infrastructure without requiring yet another ingestion layer.

4. RICH VISUALIZATIONS AND DASHBOARDS

Superset ships with a wide array of beautiful visualizations. Our visualization plug-in architecture makes it easy to build custom visualizations that drop directly into Superset.

### Why Superset is production ready and can be compared to various BI tools like Quicksight and Power BI and Metabase

1. ROW LEVEL SECURITY:

Superset allows us to manage access to the different rows in a particular database or table by giving the flexibility of specifying a field or column for which access is to be denied.

**USE CASE** :

Assuming we have a table from a database containing branch level data (1 lakh records) as the unique key, and if we have to generate analytics for each branch then that would mean we have to generate 1 lakh dashboards. Superset helps us to easily manage this scenario by allowing us to specify the various roles and the access to the data, which means that we can create a single dashboard and create views to the different users based on the roles.

2. GRANULARITY IN PERMISSIONS:

Superset offers us the flexibility of creating ROLES and specifying the permissions for each role. There are multiple drag and drop permissions which can be easily added to a CUSTOM role ensuring fine granularity in the permissions.

**USE CASE**:

When we have a large number of parties who want various views on a particular dashboard it becomes very difficult to create them. Hence Superset offers a granular approach based on ROLES which allows the admin to manage the groups and assign the users to the particular group as and when they are created.

3. AUTO MAILING FEATURE AND SHARING OF DATA:

Superset allows us to configure mailing services which automates the entire process of creation to sharing of data to the respective stakeholder’s email.

**USE CASE**:

It is often difficult to share the dashboards in a standard format when there a large number of parties involved. Hence in Superset we can give the features of auto mailing which allows the admin to automate the sending and mailing of the dashboards.

4. INTEGRATION WITH ACTIVE DIRECTORY

Superset allows us to integrate with various authentication services and integration with Active Directory using the LDAP protocol.

**USE CASE**:

If a company has > 100 employees, managing and creation of permissions with Row Level Security Manually for each of the records is a time consuming process and data entry errors are a pain to deal with

5. DATA REDUNDANCY AND AVAILABILITY:

There are currently three ways of deploying Superset
• DOCKER
• KUBERNETES
• PIP INSTALL

**USE CASE**:

Scalability is a major concern as the number of users increases which usually causes slow run times as and when the number of users increases. Hence the power of Kubernetes allows us to manage multiple deployments of docker images on the cloud and also allows up to orchestrate and spin up containers as the traffic increases, which ensures fast load times and improves the User Experience.

6. SQL LAB

SQL Lab allows us to directly connect the data sources from a variety of data sources and this connection allows us to prototype the various tables in real time.

**USE CASE**:

When we have to create a visualizations, it is often done using Query logic. Hence Superset allows us to view the data, run the query and also visualize the prototype in a single window, this helps the developers to increase the productivity as all the information is available.

### Installing Superset

There are mainly three methods of installing Superset according to the documentation as mentioned above and here we are installing it on and EC2 Instance from AWS on a DOCKER IMAGE.

1. Let’s set up the EC2 Image on AWS

- Register with a free AWS account and navigate to the respective EC2 page and launch a free tier micro instance
- Let’s set up the EC2 Image on AWS

![AWS Console](https://user-images.githubusercontent.com/28874545/154719725-6129b0cf-c005-4c6d-9ed0-d74ab1cb590b.png)

- After clicking on SELECT in the image above leave all the options as default and the CONFIGURE SECURITY GROUP TAB we need to open port 8088 as Superset runs here as shown in the image below.

![image](https://user-images.githubusercontent.com/28874545/154720235-d7c17027-f81d-4d78-b602-7d199b6b9d5f.png)

- Login to the instance and proceed to install the docker image

2. The next step is to install DOCKER COMPOSE and DOCKER ENGINE from the links below for an ubuntu instance

- Docker Engine : https://docs.docker.com/engine/install/ubuntu/
- Docker Compose: https://docs.docker.com/compose/install/

3. Then we can install Superset according to the documentation below:
   https://superset.apache.org/docs/installation/installing-superset-using-docker-compose

![image](https://user-images.githubusercontent.com/28874545/154720586-38286035-aeec-4da1-a751-112441aa01e6.png)

Now if we want to add a connector to a specific database then before the command

$ docker-compose -f docker-compose-non-dev.yml up

We need to install the respective connector as given in the link below ,

https://superset.apache.org/docs/databases/dockeradddrivers
Here in our use case we need to install the Athena driver hence in the command,

$echo “mysqlclient” >> ./docker/requirements-local.txt

We need to replace “mysqlclient” with “pyathena” and the complete list of drivers can be found in the link below :
https://superset.apache.org/docs/databases/installing-database-drivers

![image](https://user-images.githubusercontent.com/28874545/154720911-ab2dc520-ceef-4ea8-9953-7483016ccff8.png)

Once Superset is installed we can login using the default user name and password which is admin : admin

### Row Level Security on User Level

Row level security provides an easy way to manage access to the various roles and permissions and access to the fine grained data. This can be implemented by going into the SETTINGS ICON and selecting the ROW LEVEL SECURITY as shown in the figure below

![image](https://user-images.githubusercontent.com/28874545/154721354-72261ca0-ef43-4517-97b9-06ee9f325182.png)

Then click on new (+) icon on the right side and select all the fields that need to be added as shown in the image below :

![image](https://user-images.githubusercontent.com/28874545/154721480-489a963c-f4d9-425a-862c-b09cbe79ecd5.png)

Then we can add a new user and specify this ROLE for them which ensures that the row level security is implemented and that they can see only those Records to which they have access.

### Row Level Security on Data Set Level

**USE CASE :**

If we have a business in which there are about 10000 users and these users are a part of 100 branches and if we have to display a dashboard in such a way that only the current branch user can view their performance in the current quarter. i.e Each branch user must be able to view only their Branch performance and not other branches.

**Solution:**

We have to manually set the Row level security for each user based on their user name as shown in the image below. Not only this, but also we need to manually add all the tables in the ROLE section for a particular user. In the future if we have more tables then we need to manually add them to the row level security as well.

Although the documentation is not clear on how to solve this issue after a lot of research we found that there is a built in DYNAMIC FILTERING OPTION using the JINJA TEMPLATE. The line below uses the template to give the current username and this helps us to filter later in the DASHBORD LEVEL  
'{{current_username()}}'

This needs to be enabled,

1. We need to login to our EC2 instance and locate the superset docker folder.

2. Next we need to go to /superset/superset/config.py

3. If we open this file using nano and then search using ctrl+w ENABLE_TEMPLATE_PROCESSING, we can see that it is set to false

![image](https://user-images.githubusercontent.com/28874545/154721969-0a9bef9e-7b40-4166-9a26-fa98c7904045.png)

4. Even though we set it to true it does not allow us to make any changes as superset is designed in such a way that we have to override this by making changes in another file called
   superset_config.py.

![image](https://user-images.githubusercontent.com/28874545/154722120-d89f1115-8ee1-4177-b24b-9fdcd10831e7.png)

5. What ever changes we make in this file is overwritten in the file called config.py.

6. To enable template processing we need to check the config.py

![image](https://user-images.githubusercontent.com/28874545/154722229-aa75bba3-a677-44a5-beed-4b01b67cb416.png)

7. It tells us to change the FEATURE_FLAGS to TRUE. Open /superset/docker/pythonpathdev/superset_config.py and search for FEATURE_FLAGS . Then in a new line enable template processing and restart the instance.

![image](https://user-images.githubusercontent.com/28874545/154722338-a85a202c-dd21-4658-aba7-d7184a2a3d12.png)

8. Once we restart the instance we can create a dataset in which we have a unique user name.

![image](https://user-images.githubusercontent.com/28874545/154722456-016ca85c-ae85-4f1c-ac95-6008baaa9edd.png)

9. Here we need to select edit dataset and then choose the legacy sql editor.

![image](https://user-images.githubusercontent.com/28874545/154722706-27052659-ce5f-48a4-a277-a93800fb3067.png)

10. Then paste the string based on your use case. Here we want only the logged in user to view the current dashboards containing his/her username and not the dashboards of other users.

### Refreshing a Dataset:

Since we have enabled Athena Driver on the superset instance, if we have created dashboards on superset and if we change the source database or reload the data it causes issues in superset as old dashboard does not reflect the new dataset.

This issue can be solved by,

1. Clicking on edit dataset and navigating to the columns part

![image](https://user-images.githubusercontent.com/28874545/154722882-53b70c52-a144-4867-8980-0b62f93ddb1f.png)

![image](https://user-images.githubusercontent.com/28874545/154723088-4faafa59-d5bc-4f7d-b131-cbebb95163c8.png)

2. Now if we click on Sync Columns from source all the old dashboards will reflect the new dataset.

## Increasing Storage on EC2 as the datasets increase:

Go to the console, and choose the volume, then go to modify and change the storage. This can only be increased and once done we cant downgrade.

![image](https://user-images.githubusercontent.com/28874545/154723392-9f076929-ccad-4f2d-8fe7-e1183e0f25a1.png)

We then need to manually allocate the storage on the ec2 instance.

$ Df -Th
This command is used to get the increased volume in this case it is XVDA
$growpart /dev/xvda 1
This will increase the partision
$resize2fs /dev/xvda1

## Increasing Storage on EC2 as the datasets increase:

The analyics can be viewed in the SQL lab:

It is present under the PGSQL database, Schema: Public, table ab_user

Query : SELECT \* from ab_user where EXTRACT(MONTH FROM last_login )=10

![image](https://user-images.githubusercontent.com/28874545/154723908-0be2af80-b34f-4343-ae18-0ed4fb26f8b9.png)

### Embedding Dashboards on Another Application:

First, you need to update the PUBLIC ROLE under Settings with these options.

- can explore json on Superset
- can dashboard on Superset, all database access on all_database_access.
  Second, embed your dashboard in your HTML

<iframe src="localhost:8088/superset/dashboard/5/?standalone=true"></iframe>
Here ‘5’ in the URL specifies the dashboard number

### Creation of Datasets:

To create a Dashboard we need to follow the steps below:

1. Go to the DATA tab
2. Select create a DATASET button as shown in the image below

![image](https://user-images.githubusercontent.com/28874545/154724204-d241d9b3-6669-4bab-96cb-a48bc013915d.png)

3. Select the database, the schema, and the table name

4. Then choose the dataset and select the visualisation type as TABLE

![image](https://user-images.githubusercontent.com/28874545/154724420-5bea0458-d7a0-4b27-9f70-128cf013e208.png)

5. Add all the respective fields and run the query. After that save the result in a new DASHBOARD.

![image](https://user-images.githubusercontent.com/28874545/154724546-fb2cb612-5dbf-45f6-bd95-0d535c0f7e5c.png)

### Backup and Restore Superset Via Docker

A docker image does not have persistent storage hence when the image is torn down or if the image crashes the entire persistent data stored in the DB will be terminated.
We can find out more from the blog: https://docs.docker.com/storage/volumes/

![image](https://user-images.githubusercontent.com/28874545/154724701-3d5d5e57-0b73-4a31-907d-0b9b122b5a80.png)

Hence If we need to take backups of the data, it is crucial to identify the mounting point of the docker image on the Operating System and on Ubuntu this can be found in the /var/lib/docker.
STEPS TO BACKUP AND RESTORE A DATA IN DOCKER

1. Create a copy of the current volume

Cp -r [source] [destination]
Here since we already have a backup in backup_vol we are copying it into /var/lib/docker

$ sudo cp -r /home/ubuntu/backup_vol/docker /var/lib/docker

2. Stop the services as well:

$sudo service docker stop

3. Stop docker containers by using the command

$ sudo docker stop $(sudo docker ps -q)

Make sure all the services show as exited and this takes a bit of time

Recheck by running
$docker ps -a-non

![image](https://user-images.githubusercontent.com/28874545/154725127-863c24cf-f729-4de3-b010-cc2d4e3ef03d.png)

4. Stop containers and remove containers, networks, volumes, and images created by up.

$ sudo docker container down

5. For testing purposes remove the current docker volume which is present in the file system by running
   $ sudo su
   $ cd /var/lib
   $ rm -R docker

6. If the device is busy then we need to use umount command.  
   $umount overlay
   By doing this all the persistent data from the disk has been removed including the row level permissions that we had set.

![image](https://user-images.githubusercontent.com/28874545/154725218-62e12c96-2316-4819-8547-82744036eb88.png)

![image](https://user-images.githubusercontent.com/28874545/154725310-c7d8c802-597c-48da-ab35-73df146f3d44.png)

Here there is no user with the row level security .

7. Now we have a backup in the home folder, which needs to be copied to /var/lib/docker

sudo cp -r /home/ubuntu/backup_vol/docker /var/lib/

Here the name of the backup is docker in the folder backup_vol

![image](https://user-images.githubusercontent.com/28874545/154725420-a654732b-d647-40dd-89bb-ccde32397b9f.png)

8. Now we need to restart it as it will cause errors as it will be reading the data from /var/lib/docker

Now use docker compose up and restart from scratch

$ sudo service docker restart
$ sudo docker-compose up

If we get errors ctrl+c then wait for the service to go down, then go to the main superset folder and run the main command to start superset.

$ cd superset
$ sudo docker-compose -f docker-compose-non-dev.yml up

This ensures that the volumes will be read from the correct location from the backup folder.

9. This data needs to be backed up to S3 layer as well this can be done by using the tar command.
   $cd /var/lib
   tar -zcvf name_of_file_to_be_saved folder_name

• -z : Compress archive using gzip program in Linux or Unix
• -c : Create archive on Linux
• -v : Verbose i.e display progress while creating archive
• -f : Archive File name

$tar -zcvf prev_backup.tar.gz /var/lib/docker

10. Then we need to install the AWS CLI,
    https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html
    After this we need to send the data to the S3 bucket. This can be done by copying the S3 bucket URI.

To copy the files from EC2 to S3
$ aws s3 cp <Fully Qualified Local filename> s3://<S3BucketName>

Hence if we have a file called prev_backup.tar.gz and s3 bucket URI then

$ aws s3 cp /home/ubuntu s3://<S3BucketName>

Now this data is sent to the respective bucket and is stored successfully.

11. To restore this copy from S3

$aws s3 cp s3://<dataengineer-out/supersetbackup> <Fully Qualified Local filename/Directory>

Using tar unzip the file (USE SUDO SU and then UNZIP)

$ tar -zxvf prev_backup.tar.gz

$ sudo mv prev_backup/docker /var/lib

Du – display disk usage:
$du -h foldername

Df- Display file system file size
$df -f (Shows the full file system file size)

Superset Reset automation:
https://gist.github.com/pajachiet/62eb85805cee55053d208521e0bdaf13/revisions

# Automation of Superset backup to AWS.

1.Create a script called automate_backup.sh. And give necessary permissions.

$nano automate_backup.sh

This script copies the entire docker folder in /var/lib to the home directory, then compresses it

 HOME=/root LOGNAME=root PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin LANG=en_US.UTF-8 SHELL=bin/sh PWD=/root #!/bin/bash
 sudo cp -r /var/lib/docker /home/ubuntu/prev_backup 
 tar -zcvf /home/ubuntu/prev_backup.tar.gz /home/ubuntu/prev_backup/docker

 $sudo chmod 777 automate_backup.sh

2. Make sure that the aws cli is configured in the instance and the Access code and key is set.
   https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html

$nano automate_s3_storage.sh

# This script copies the zipped data from Ec2 to S3. We have to specify the s3 URI by creating a folder

aws s3 cp /home/ubuntu/prev_backup.tar.gz s3://bucket_url

$sudo chmod 777 automate_s3_storage.sh

3. Schedule the cron job to run the first script (automate_backup.sh)

   $ cron tab –e

   #this creates a local backup and it is stored as a tar file every day at 12 AM IST or 5:30am UTC

   30 5 \* \* _ /home/ubuntu/automate_backup_test.sh

   #this sends the backup to aws on every seventh day at 12 AM IST or 5:30 am UTC

   30 5 _ \* 0 /home/ubuntu/automate_s3_storage.sh

   #check the status of the cron tab

   $ cron tab -l

By following all these steps the data is successfully backed up into s3 on a periodic basis. Due to the compression the size of the file is reduced by a factor of 4. (15 GB file is reduced to 3.7Gb)
