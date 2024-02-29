# GitHub Actions

This repos is to demo how we can trigger github actions. It automates the building of a Docker image from the repository's source code, generates a deployment package, and deploys it to AWS Elastic Beanstalk upon pushes to the main branch or pull requests targeting the main branch.

This GitHub Actions workflow, named "Docker Image CI," is triggered on pushes to the main branch and pull requests targeting the main branch. 

## Build Job:

1. This job runs on an Ubuntu latest runner.

2. It checks out the source code using actions/checkout@v2.

3. It builds a Docker image named "ml_project" using the provided Dockerfile in the repository root directory.

4. It generates a deployment package by compressing all files in the repository into a zip file named "deploy.zip".

## Deploy to EB:

This step uses the einaregilsson/beanstalk-deploy@v14 action to deploy the built Docker image to AWS Elastic Beanstalk.

1. It requires AWS credentials (AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY) stored in GitHub Secrets for authentication.

2. It specifies the AWS Elastic Beanstalk application name as "MLProjectFinal", the environment name as "MLProjectFinal-env", and the version label as "MLProjectFinal".

3. The deployment is targeted to the "eu-north-1" region.

4. The deployment package provided is the "deploy.zip" generated in the previous step.


