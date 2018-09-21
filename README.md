# aws-cloudformation-rds-docker

Automated way to create EC2, RDS instance and deploy docker container with postgres container

# Prerequisites
- Configure AWS CLI
- Create a key pair in EC2 instance
- Download the pem key
- Change the permission of pem key using chmod 400
- Copy the pem key to aws-rds-automate.pem
- Get the value of ubuntu AMI id from launch instance screen and replace in stack.yml at ImageId parameter


# Deploy aws cloud formation template
```aws cloudformation create-stack --stack-name potgres-rds-docker --template-body file://stack.yml```

# Update docker-compose.yml 
- Take the endpoint from AWS RDS instance and update in docker-compose.yml file on DB_HOST parameter

# Deploy docker single node container in DB instance
```docker-compose -f docker-compose.yml up -d```

# Check the docker containers running
- export DOCKER_HOST=```public ip address of EC2 instance```
- Example ```docker -H tcp://54.245.186.56:2375 ps -a``` will display all the containers running inside the host


# SSH to server and run all the below commands one by one
- ssh -i location-to-pem-key ubuntu@publicipaddress
- sudo su
- docker ps
- docker exec -it containerid bash
- apt-get install postgresql-client
- psql postgresql://postgres:postgres@localhost:5432/postgres
- select schema_name from information_schema.schemata;
- press ctrl + z
- kill %%







