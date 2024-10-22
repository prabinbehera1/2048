# Deploying 2048 Game on AWS Elastic Beanstalk with Docker

This guide will walk you through the process of deploying the popular 2048 game on AWS Elastic Beanstalk using a Docker container. AWS Elastic Beanstalk is a fully managed service that makes it easy to deploy and run applications in multiple languages.

## 2048 game

<img src="2048win.jpg"/>

## FLOWCHART

<img src="Screenshot from 2023-07-03 19-51-41.png"/>

## Prerequisites

Before you begin, make sure you have the following:

- An AWS account with the necessary permissions to create and manage Elastic Beanstalk environments.
- Docker installed on your local machine. You can download and install Docker from the [official Docker website](https://www.docker.com/get-started).

## Step 1: Clone the Repository

Start by cloning {master.zip} the 2048 game repository to your local machine:

```bash
https://github.com/prabinbehera1/2048/archive/refs/heads/master.zip
```

## Step 2: Create a Dockerfile

In the root directory of the cloned repository, create a file named `Dockerfile` and open it in a text editor. Add the following content:

```Dockerfile
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y nginx zip curl
RUN echo "daemon off;" >>/etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://github.com/prabinbehera1/2048/archive/refs/heads/master.zip
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip
EXPOSE 80
CMD ["/usr/sbin/nginx","-c","/etc/nginx/nginx.conf"]
```

Save the `Dockerfile` and close the text editor.

## Step 3: Build the Docker Image

Open a terminal or command prompt and navigate to the root directory of the cloned repository.

Build the Docker image using the following command:

```bash
docker build -t 2048-game .
```

This command builds the Docker image using the `Dockerfile` in the current directory and tags it as `2048-game`.

## Step 4: Test the Docker Image Locally

To ensure that the Docker image is working correctly, you can run a container locally.

Start a container based on the image you built:

```bash
docker run -p 80:80 2048-game
```

The container should start, and you can access the 2048 game by opening a web browser and navigating to `http://localhost:3000`.

## Step 5: Create an Elastic Beanstalk Application

Go to the [AWS Management Console](https://console.aws.amazon.com/) and navigate to the Elastic Beanstalk service.

Click on "Create Application" and follow the prompts to create a new application.

## Step 6: Create an Elastic Beanstalk Environment

In the Elastic Beanstalk console, click on "Create environment" and select "Web server environment."

Configure the environment as needed, providing a name, description, and selecting the desired platform. Choose the platform that matches your Docker image.

In the "Base configuration" section, select "Upload your code" and click on "Local file." Choose the Docker image tarball you created earlier.

Click "Create environment" to launch the environment.

## Step 7: Access the Deployed 2048 Game

Once the environment is created, Elastic Beanstalk will begin deploying your Docker image. This process may take a few minutes.

After the deployment is complete, you can access the deployed 2048 game by navigating to the environment's URL provided in the Elastic Beanstalk console.

Congratulations! You have successfully deployed the 2048 game on AWS Elastic Beanstalk using a Docker container.

## Conclusion

In this guide, you learned how to deploy the 2048 game on AWS Elastic Bean

stalk using a Docker container. You can now customize and enhance your deployment as needed to suit your requirements. Enjoy playing the game!
