# AWS-RDS_MYSQL-AUTOMATION-WITH-BOTO3-AWS_SSM

In this repo I will show how to create and connect to  a mySQL DB running on AWS RDS. The automation job will consist on inserting records to the DB and connect to it with python; for last we will introduce a way to secure sensible information with AWS SSM -Secrets manager- that I will utilize as a secret store for the RDS's enpoint, user and
password.

1. We will create a DB that will be only accesible from an specific VPC, meaning that the RDS Database will only accept connections originating from a private IP attached to one of our EC2 instances.

![image](https://user-images.githubusercontent.com/32818490/117994026-3aa8ff00-b30e-11eb-9b13-d1be8a9997e1.png)

Image 1. Architecture part 1.

Image 1 shows the initial architecture for the infrastructure that will be deployed in this tutorial. On image 2, I will add a method for securing DB's sensible authentication information.

![image](https://user-images.githubusercontent.com/32818490/117996661-544b4600-b310-11eb-8e05-45a1bdb5e47f.png)

Image 2. Architecture part 2.

The following are the required steps to deploy a MYSQL DB with AWS RDS.

1. Go to AWS CONSOLE > RDS DATABASE > CREATE DATABASE.
2. Select MySQL engine as show below.

![image](https://user-images.githubusercontent.com/32818490/117997490-0256f000-b311-11eb-8496-f4045311efae.png)

Image 3. MySQL Engine for RDS

3. Select a free tier RDS for testing purposes and set up user and password for your DB

![image](https://user-images.githubusercontent.com/32818490/117997772-46e28b80-b311-11eb-95ad-4f184eb2b208.png)

Image 4. Free tier elegible, user/password

4. Make sure you put No as public access

![image](https://user-images.githubusercontent.com/32818490/117997980-772a2a00-b311-11eb-877a-c8dd64a72633.png)

Image 5. Deny public access to DB

5. Click create


