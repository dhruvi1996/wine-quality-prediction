//CS 643 Cloud Computing 
//Dhruvi Makadia 
// Programming Assignment 2
# Wine Quality Prediction | Assignment 2

Goal: The purpose of this project is to train a machine learning model parallely on ec2 instances for predicting wine quality on a piblically available data and then use the trained model to predict the wine quality.
Project also uses Docker to create a container for trained machine learning model to simplify deployments.

## Full Readme 
* [Readme word](https://github.com/dhruvi1996/wine-quality-prediction.git)
## Docker image link
* [Docker image : dhruvi11/aws-winepredictionmodel](https://hub.docker.com/repository/docker/dhruvi11/aws-winepredictionmodel)

## Before running Requirements :
* Input files must be copied under data/ and with same name TestDataset.csv
* Input file must have save format as of TrainingDataset.csv and ValidationDataset.csv. 
* Column names in double quotes with exact name number of column with same names and separator ';'

## Docker run instructions
````
docker pull dhruvi11/aws-winepredictionmodel
docker run dhruvi11/aws-winepredictionmodel
docker run --platform=linux/amd64 dhruvi11/aws-winepredictionmodel testFilePath

Docker run -v [fullLocalPath of TestDataset.csv: data/TestDataset.csv ]  dhruvi11/aws-winepredictionmodel
for e.g. Sample command : 

docker run -v /Users/<username>/<Desktop>/<path-to-folder>/TestDataset.csv:/data/TestDataset.csv dhruvi11/aws-winepredictionmodel

````
