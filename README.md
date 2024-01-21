# WordPress Website on AWS

### <U>VPC CREATION</U> 

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/e09d9bdd-7671-434f-945b-2ddd8f28e725)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/fc20a991-d941-4a5b-8439-62cd8d36de19)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/820b5107-4ca0-4525-99dc-5d8dea668b47)

>[!note]
>Once a VPC is created a default route table is created. And by default the route table is private.

### <U>CREATE INTERNET GATEWAY AND ATTACH IT TO VPC</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/f1e6a6b4-ade3-46dd-9aee-7c6fe739e151)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/015101b3-e082-4de9-9a22-276b79f6176c)
After creating the internet gateway, attach it to the VPC that was created. Select the IGW and click on Actions -> Attach VPC.

### <U>CREATE PUBLIC SUBNETS IN 2 AVAILABILITY ZONES</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/1d5f4363-bcd1-4ce8-a099-c4d356eecea5)
>[!IMPORTANT]
>Always make sure to select the appropriate VPC, currently in the wp-app VPC there are no subnets.

<u>Public subnet-1</u>
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/8212cb0e-fb8d-4525-a4a0-4923e3033b2f)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/23fd3e87-cea4-4fe5-bac3-596c15aab659)

<u>Public subnet-2</u>
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/fd4798e2-afea-489f-a00f-7c63363f90ca)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/b65058c5-13c4-414f-8fb4-04a29ec530f6)
>[!Note]
>Please note that the availability zone should be us-east-1 and the CIDR block should be changed accordingly.

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/0db0abe4-849b-46e9-9cd8-cde9a31a2b6f)
>[!NOTE]
>Select a subnet and click on Actions -> Edit subnet settings and select Enable auto-assign public IPV4 address.
>We can also do this while creating an EC2 instance in which the Enable public IP address option can be enabled.

### <U>CREATE PUBLIC ROUTE TABLE</U>

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/ae2dbbf9-c0b9-4d88-b3f8-1663cee71f4d)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/c288d9a5-82a1-4bd3-8956-05196c97308c)
>[!Note]
>Select the route table and click on Actions -> Edit Route table. Here the Destination shall be anywhere in the internet and the target shall be Internet gateway.

![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/83dded57-839d-4e23-98d1-13a82f40091a)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/6cb9fc13-27c3-47c6-b27f-3d866438fd07)
![image](https://github.com/karthi770/API-Gateway-with-Lambda/assets/102706119/77c1ca49-8d37-4879-8534-e7118392f1c8)
>[!Note]
>Click on the Edit subnet Associations.
>Select both the subnets and click on save.
### <u>CREATE PRIVATE SUBNETS</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/049f5aa6-bdb8-41ac-a03a-7de26ee3df30)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/bcc10ad0-7f37-4404-8dda-40219ee64203)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/27f4d23a-74d9-44cc-bd7e-8b1c61a0ff48)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/a7343068-c5f4-4c3a-9bc5-bd80aa7a4bf1)
>[!Note]
>There are 2 private subnets each in one availability zone for the application.
>Another 2 private subnets each in one availability zone for the Database.

### <u>CREATE PRIVATE ROUTE TABLES</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b5f2a7bb-3e13-4b12-8f3b-999efb62f4ea)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7b3dbb59-59a9-46e3-87a1-c41e2337d3d8)
>[!note]
>Create private route tables with no internet gateway attached to it. Private subnets don't have internet access.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/cbb3c3b3-e019-4f89-b351-57d1abd78ec0)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7f53b7ac-4e4c-4caa-bc97-1a1c0f55b30e)

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/dd5b34d2-b9b7-441d-84ed-522cce4a51e6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/1569583e-2541-4f8a-b868-13bcf1d6c8ce)
>[!note]
>Private subnet 2 is connected to the default route table that was created during the VPC creation. If we look into the column name "Main" it says "Yes", which means it is associated to the main route table.
### <u>CREATE NAT GATEWAY</u>

>[!INFO]
>NAT (**Network Address Translation**) Gateway allows the private subnets to have internet access to download packages. However the external services cannot initiate a connection with those instances.
>

>[!important]
>NAT gateway is always created in the public subnets.
>Before you create the NAT gateway make sure you are in the appropriate region 
>(ex: us-east-1)

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/857fcd53-513f-4508-8ff1-a2fcdd4d643e)
>[!Note]
>Create elastic IP addresses just by clicking on the "Allocate Elastic IP address" and there is not much settings to change inside it. 
>There will be 2 NAT gateways for each public subnet, that is why 2 IP address.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/6478f0f8-bc44-4562-838d-3e7c0072ecb6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7c6ec6a0-2c39-46eb-b511-a829d1ea30b3)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/ecd7c54f-6441-4df8-8780-f157321f236c)
>[!note]
>In the above steps we have created a NAT gateway on the public subnet-1 and allocated a elastic IP to it.
>Next we have edited the private route table -1 and added the NAT gateway -1 to it so that the private subnet-1 can have access to the internet.
>Now do the same to NAT gateway - 2.

### <u>CREATING SECURITY GROUP</u>

>[!IMPORTANT]
>Before creating the SG we must understand that:
>- Application load balancer will accept traffic from anywhere in the internet
>- App servers will accept traffic only from the Application Load balancer
>- Database servers will accept traffic only from the App servers
>- EFS file system will accept traffic from the App servers.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/3244589f-3eff-4e82-ba56-ec7874cb8fab)
>[!note]
>This SG was created when the VPC was created. This a default one.

#### ALB Security group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/604adcfc-7a76-401c-b8fa-136d19f6c29f)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/9900d3d2-4744-4490-aa72-f851169c28f6)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/6fadb5fe-641f-4e80-89ca-80361d62327c)

#### Appserver Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/f044531e-4ba2-463a-86b2-dc0f00bade34)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/144fb4c8-0f05-4d82-88c3-9a7b0eabcc26)
>[!note]
>As mentioned above the app server will accept traffic from ALB so select the source to be ALB.
>Outbound shall be all traffic.

#### Database Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/69bf43a3-a4aa-49a1-8114-5049570ac0ac)
>[!note]
>Database shall accept traffic from App server only. and the type of database is MySql.

#### EFS Security Group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/222818a7-4381-4470-9a96-47c45f94e702)
>[!info]
>One point to be noted in EFS is, there is another inbound rule added after creating the EFS SG. The below image will show it. We have to add EFS SG as inbound rule along with App server SG.
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/e3c48011-9521-4c8b-9910-acc23076d736)

### <u>CREATING MYSQL DATABASE</u>

#### Create subnet group
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/f13f74d8-7232-4be8-b753-c9482af90d12)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/c4afe5dd-70dd-4457-971e-3afec4a3dae8)
>[!note]
>Choose the availability zone and select the subnets that were created for the database.

#### Create Database
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/8f94d4b9-7340-40a1-835e-276c1dd406f7)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/abb1a75e-4205-4314-99c8-c70888e1a735)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/4a8604b9-d747-41cb-8578-92b11640d3ef)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b5a13a8b-5874-4680-ba83-e2ded78acacb)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/2166506a-638f-41eb-a914-aeae09a1e2a3)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/60ba2aae-7fe2-483f-b449-45f39c33aad4)

### <u>CREATING ELASTIC FILE SYSTEM</u>

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/a17d104c-cddb-4240-b11e-271dfe6440e9)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b330427c-4c9d-48a7-8eed-e5cf3dce3bb7)
>[!important]
>Uncheck the enable encryption of data at rest to avoid additional charges.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/ecf8c38c-585b-4bbe-9f27-8c92b1a1c638)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/7672be7b-2861-4995-9f72-4f692c39e4b3)
>[!note]
>Make sure to select the private subnet that we created for the database.
>Make suer to select the SG that we created for the EFS.

#### Create an EC2 instance of the database
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/75174581-b8ed-4aa5-ac7c-9d976560d3fe)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/966175b3-ea47-4986-9ef1-8cb97d399404)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/b48bc1f8-ff6c-4367-b8f6-a88db945ba84)
>[!note]
>Create a new EC2 instance and select the appropriate VPC and private subnet. 
>Create a keypair so that we can ssh with the instance.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/452dca95-b668-4b0e-b885-a53960e39639)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/eafb1016-cf82-4d04-9720-499a8f17c838)
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/df547bea-4b94-4471-80f1-63ebb1fa0327)

#### Mounting the EFS
![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/615545e4-33ae-4717-ac4f-d6caa9f8faad)
>[!note]
>Get into the EFS that we created and click on "Attach". We shall get these commands. 
>Now we have to ssh in to the db instance and run these commands.

![image](https://github.com/karthi770/EC2-tagging-Boto3/assets/102706119/98c67de2-82d2-4ae9-a9c9-381f64195f70)
>[!important]
>Before we get into the mounting part, we need to make sure that the DNS hostnames is enabled in the VPC.

