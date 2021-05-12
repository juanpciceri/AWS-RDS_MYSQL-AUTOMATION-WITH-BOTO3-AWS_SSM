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

At this point you must wait for a couple of minutes for AWS to set up the environment you just configure. When the process of setting up your DB is complete, you will see the status as available for your DB.

![image](https://user-images.githubusercontent.com/32818490/117998520-fa4b8000-b311-11eb-9a6c-ebcdbfe54688.png)

Image 6. DB available.

The important information to be able to connect to his EC2 instance is the endpoint and port for connection. You could check this information on your AWS console. Sensitive information such as user and password is not shown on the AWS console interface, so make sure you kept this info secure.

![image](https://user-images.githubusercontent.com/32818490/117999010-6b8b3300-b312-11eb-8649-ae1a24c5090f.png)

Image 7. Endpoint and port for RDS instance.

From the public EC2 instance, I will try to connect to my RDS Database. for this purpose you must follow along the following steps:

1.Make sure you have configure your AWS CLI keys on AWS IAM, giving to this the least privileges; and set them up correctly on your EC2 with $aws configure command. 
2.Open a rule on the security group of the RDS instance allowing connections comming from the private IP belonging to the public EC2, the port is the one shown on figure 7.  
3.Install MySQL Client on your EC2. The command for installing is:

$sudo yum install mysql

4.Make sure python3 and boto3 library is installed if you want to follow along.
5. Connect to your DB using the following syntax.
PROMPT> mysql -h <endpoint> -P 3306 -u <mymasteruser> -p
It will ask for your password, after entering the correct password you will have the following prompt.
  
![image](https://user-images.githubusercontent.com/32818490/118001162-76df5e00-b314-11eb-8c4a-c0b5bce939c9.png)

Image 8. Connection successfull from your public EC2 to your private RDS Instance. Hurray!!

The next part of this tutorial will create a database named "movies" and a table that will contain information of movies like tittle, director, genre and year of release.
Execute the following commands to accomplish that task.

1. Create the DB "movies"

CREATE DATABASE movies;

2. Confirm the DB was created

SHOW DATABASE;

![image](https://user-images.githubusercontent.com/32818490/118004126-303f3300-b317-11eb-83d2-cc0676c39775.png)

Figure. 9 Creation of DB "movies"

3. Define tittle, director, genre and year of realse together with their data types.

In the process of creating a table, you need to specify the following information:

a. Column names – We are creating the title, genre, director, and release year columns for our table.
b. Varchar of the columns containing characters – Specifies the maximum number of characters stored in the column.
c. The integer of the columns containing numbers – Defines numeric variables holding whole numbers.
d. Not null rule – Indicates that each new record must contain information for the column.
e. Primary key – Sets a column that defines a record

Use the database movies with the following command:

USE movies;

Create a table using the CREATE command. Using the information from our movies example, the command is:

CREATE TABLE movies(title VARCHAR(50) NOT NULL,genre VARCHAR(30) NOT NULL,director VARCHAR(60) NOT NULL,release_year INT NOT NULL,PRIMARY KEY(title));


![image](https://user-images.githubusercontent.com/32818490/118004785-c5422c00-b317-11eb-898e-70f1aa5e5fe1.png)

Figura 10. Commands to define table within DB movies.





