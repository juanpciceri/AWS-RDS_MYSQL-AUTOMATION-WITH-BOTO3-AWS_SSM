# AWS-RDS_MYSQL-AUTOMATION-WITH-BOTO3-AWS_SSM

In this repo I will show how to create and connect to  a mySQL DB running on AWS RDS. The automation job will consist on inserting records to the DB and connect to it with python; for last we will introduce a way to secure sensible information with AWS SSM -Secrets manager- that I will utilize as a secret store for the RDS's enpoint, user and
password.

1. We will create a DB that will be only accesible from an specific VPC, meaning that the RDS Database will only accept connections originating from a private IP attached to one of our EC2 instances.

![image](https://user-images.githubusercontent.com/32818490/117994026-3aa8ff00-b30e-11eb-9b13-d1be8a9997e1.png)

Image 1. Architecture part 1.

Image 1 shows the initial architecture for the infrastructure that will be deployed in this tutorial. On image 2, I will add a method for securing DB's sensible authentication information.

![image](https://user-images.githubusercontent.com/32818490/117996661-544b4600-b310-11eb-8e05-45a1bdb5e47f.png)
Image 2. Architecture part 2.

