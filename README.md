
# Image Preview 

<div align=center>
<img src="https://i.ibb.co/W0K6YBm/green-blue.jpg" title="green blue" alt="Green Blue">
</div>

# Green Blue Deployment - Udacity  Cloud DevOps Nanodegree program.

> Diego Arostegui - 5/31/2020

> Capstone Project Overview


## Cluster Installation (use the Jenkins file or run)

Linux:

```sh
eksctl create cluster \
						--name thecluster \
						--version 1.16 \
						--nodegroup-name capstone-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-east-1 \
						--zones us-east-1a \
						--zones us-east-1b \
						--zones us-east-1c \
```

## Usage example

This will create an Nginx Blue version that will be replaced by a green one (sounds easy...)

## Release History

* 0.0.1
    * Working version (does green and blue)
