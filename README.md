# -Migrate-Data-into-Amazon-RDS-Database-with-Flyway

>"In this project, you will learn how to migrate data into an Amazon RDS Database using Flyway. We will be migrating data into an Amazon Relational Database Service (RDS) database and storing the code in an S3 Bucket."

Step1: Create The Ec2 Instance (ubuntu or linux)
step2: next create IAM user and Role create Accesskey and Secreatkey
Step3: select ec2 instances ---> click on Actions --click on Security -- Select Modify IAM Role -- "Attach Role"
step4: Create "RDS"
step5: Before creating the RDS add -- Create DB Subnet grouptep6: Next Go To Database --Create Database --Seletct standard create --Seletc MYSQL --Select MYSQL Version(Latest8.0.35)
       select Template here 3 options(Production or DEV/TEST or Free tier
step6: Select Deployment Options
        1.Multi-AZ DB Cluster
        2.Multi-AZ DB instance
        3.Single DB instance
step7: seletc Settings	
step8: select Credentials Settings --Master username -- click on Auto generate password OR you can provide your own
step9: Next Select Instance Configuration 3 options
       1.Standard classes (includes m classes)
	   2.Memory optimized classes (includes r and x classes)
	   3.Burstable classes (includes t classes) 
	   you can select as your reqiurement.
	   
step10: Next Connectivity Information
        Select Your VPC --Select Public access (YES or NO)-- Next Security Group(crate seperate security Group For RDS open MYSQL port 3306)
Step11: Finally create Database
NOTE: RDS will create endpoint we can integrate with your application

Step12: Connect to Ec2 instance and install "AWSCLI" and add Accesskey,Secreatkey
COMMANDS: sudo apt-get update
          sudo apt upgrade
		  sudo apt install awscli
		  aws --version
		  aws configure
		  Enter - Accesskey,Secreatkey

Step13: Download the flyway tarfil 
       - wget -qO- https://download.red-gate.com/maven/release/com/ay-commandline/10.10.0/flyway-commandline-10.10.0-linux-x64.tar.gz | tar -xvz &&lyway-10.10.0/flyway /usr/local/bin
	   - flyway-10.10.0 -- (directory is created)
       - Folder Structure- README.txt  assets  conf  drivers  flyway  flyway.cmd  jre  lib  licenses  rules 
       - Create sql directory --> mkdir sql --cd sql-- (Download S3 bucket files in to this directory or sql data)
	   
Step14:  Create S3 Bucket --- upload files in to that bucket -- click on file -- copy the URL 
	    - in terminal execute command  aws s3 ls --- it will show the s3 bucket information list	   
	    - aws s3 cp <s3Url> /localpath/directory
	    - aws s3 cp s3://myawsmigration/V1__rentzone-db.sql /root/flyway 
		
step15: finally migrate the data execute this command

flyway -url=jdbc:mysql://rdsflyway.cxmc4yyec335.us-east-1.rds.amazonaws.com:3306/RDSflyway \
  -user=admin \
  -password=plBCS4Q5dpl3cD7ft9Zd \
  -locations=filesystem:sql \
  migrate
  
 Step16: finally we done output
 Flyway Community Edition 10.10.0 by Redgate

See release notes here: https://rd.gt/416ObMi
Database: jdbc:mysql://rdsflyway.cxmc4yyec335.us-east-1.rds.amazonaws.com:3306/RDSflyway (MySQL 8.0)
Schema history table `RDSflyway`.`flyway_schema_history` does not exist yet
Successfully validated 1 migration (execution time 00:00.058s)
Creating Schema History table `RDSflyway`.`flyway_schema_history` ...
Current version of schema `RDSflyway`: << Empty Schema >>
Migrating schema `RDSflyway` to version "1 - rentzone-db"
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
WARNING: DB: Integer display width is deprecated and will be removed in a future release. (SQL State:  - Error Code: 1681)
Successfully applied 1 migration to schema `RDSflyway`, now at version v1 (execution time 00:04.344s)
