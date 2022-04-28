# wine-quality-prediction 
# Programming Assignment 2

The purpose of this project is to train a machine learning model parallely on ec2 instances for predicting wine quality on a piblically available data and then use the trained model to predict the wine quality.
Project also uses Docker to create a container for trained machine learning model to simplify deployments.

## Full Readme
Detailed step by step readme document is found here 
* [Readme word](https://github.com/dhruvi1996/wine-quality-prediction.git)
## Docker image link
* [Docker image : dhruvi11/aws-winepredictionmodel](https://hub.docker.com/repository/docker/dhruvi11/aws-winepredictionmodel)

## Steps:

### Task 1: How to create Spark cluster in AWS ?

1.After logging into AWS console, user can create cluster using EMR console provided by AWS.

2.Following are the steps to create one with 4 ec2 instances 
First create a Key-pair for EMR cluster and download .pem key. We will need it later on.
 EC2-> Network & Security -> Key-pairs

3. We must fill in respective sections:

```
   General Configuratin -> Cluster Name 
   Software Configuration-> EMR 5.33 , do select 'Spark: Spark 2.4.7 on Hadoop 2.10.1 YARN and Zeppelin 0.9.0' option menu.
   Harware Configuration -> Make instance count as 4
   Security Access -> Provide .pem key created in above step.
   Rest of parameters can be left default.
 ```
 4. If the cluster status is 'waiting' we can know successful cluster creation is done.
 ### Task 2: Parallel training on 4 ec2 Instances
 1.As we conclude that cluster is successfully created, and ready we perform SSH to Master of cluster using command:
 ```
        ssh -i "ec2key.pem" <<User>>@<<Public IPv4 DNS>>
        
```
2.We will Copy files to HDFS; Doing this, all the slave nodes can access them too.
3.We will use following command to launch apache-spark on EMR cluster.
```
	spark-submit winequality-1.0.jar
```
4.In order to use these training files all of them should be in a zip and transferred to local machine environment which we can use to predict on ec2.

### Task 3:Run trained ML model locally without docker

1.EC2 instance Create and its configuration 
```
        ssh -i "ec2key.pem" <<User>>@<<Public IPv4 DNS>>
```
2.Install Scala and Spark and also making changes for PATH environment variables.

3.uploading trained model and jar files

4.**Run wine-predict application :**
```
spark-submit wine-quality-predict-1.0.jar
```
### Task 4: Predict wine quality using docker
1. Installing docker 
2. Creating public image and post on DockerHub. Use the command **docker pull dhruvi11/aws-winepredictionmodel** to get the image on your machine.
3. docker run -v {directory path for data }:/code/data/csv dhruvi11/aws-winepredictionmodel {testdata file name}
4. docker run --platform=linux/amd64 dhruvi11/aws-winepredictionmodel testFilePath; by giving this command the docker will run specifically on the mentioned platform .
## Docker run instructions
````
docker pull dhruvi11/aws-winepredictionmodel
docker run --platform=linux/amd64 dhruvi11/aws-winepredictionmodel testFilePath

Docker run -v [fullLocalPath of TestDataset.csv: data/TestDataset.csv ]  dhruvi11/aws-winepredictionmodel
for e.g. 
Sample command : 
docker run -v /Users/<username>/<Desktop>/<path-to-folder>/TestDataset.csv:/data/TestDataset.csv dhruvi11/aws-winepredictionmodel
````
