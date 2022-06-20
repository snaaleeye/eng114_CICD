## What is CI, CD and CDE?

Continuous Integration (CI): Developers merge/commit code to master branch multiple times a day, fully automated build and test process which gives feedback within few minutes, by doing so, you avoid the integration hell that usually happens when people wait for release day to merge their changes into the release branch.

Continuous Delivery (CD) is an extension of continuous integration to make sure that you can release new changes to your customers quickly in a sustainable way. This means that on top of having automated your testing, you also have automated your release process and you can deploy your application at any point of time by clicking on a button. In continuous Delivery the deployment is completed manually.


Continuous Deployment (CDE) goes one step further than continuous delivery, with this practice, every change that passes all stages of your production pipeline is released to your customers, there is no human intervention, and only a failed test will prevent a new change to be deployed to production.

<img width="734" alt="Screenshot 2022-06-16 at 11 43 47" src="https://user-images.githubusercontent.com/105854053/174053672-0df6beb5-a50b-40bc-bec3-941d35fc18a8.png">

https://medium.com/@ahshahkhan/devops-culture-and-cicd-3761cfc62450


## What is the difference between CD & CDE use cases?

CD is an extension of CI and CDE is a further extension of CD. While CI focuses on helping developers by ensuring each bit of new code is bug-free and functional, CD is more about releasing updates and changes in a quick and safe manner. CDE is about creating a unified pipeline for software releases and increasing the velocity of delivery. Combining all three means that when new source code is committed it can be deployed to production automatically and within minutes (or even seconds!), assuming it passes all the relevant tests. 

Example: Films during covid
Continuous Delivery, planned, desiged, pushed, tested, passed. 
Unable to deploy to cinemas - needed to add more to movies to compete. 

Example: Banks 
Service maintenance, app will be down. Ready to deploy but do not want to 
deploy on normal days and wait until nights/weekends. 

Example: Can't stop service
Amazon, Facebook, Netflix never down - Cannot afford to take service down 
and add feature and release. They use CICD to stay active.

Example: Facebook, Whatsapp, Instagram down due to CDE.
A bug was used in the CDE that took down the servers and took 6 hours to 
fix. 

<img width="749" alt="Screenshot 2022-06-16 at 11 59 24" src="https://user-images.githubusercontent.com/105854053/174056100-9f0fbdf3-46ac-4493-966b-1c1ac275bcb2.png">


## What is Jenkins?

Jenkins is an open-source automation server in which the central build and CI process take place, It is a Java-based program with packages for Windows, macOS, & Linux.

Great range of plugins available, Jenkins supports building, deploying, and automating for software development projects, easy installation, simple and user-friendly interface, extensible with huge community-contributed plugin resource, easy environment configuration in user interface & supports distributed builds with master-slave architecture.

<img width="1208" alt="Screenshot 2022-06-16 at 11 56 39" src="https://user-images.githubusercontent.com/105854053/174055705-4ed83bb4-fc38-4f30-9365-5dd58808e11e.png">


## What are the benefits of CICD pipeline?

Make sure to check cost-benefit analysis

1. Reduce risk

With a CI/CD pipeline, you can test and deploy code more frequently, giving testers the ability to detect issues as soon as they occur and to fix them immediately. You are essentially mitigating risks in real time.

2. Deliver faster

Organizations are moving toward releasing features multiple times a day. This is not an easy task; only a handful of companies like Netflix, Amazon, and Facebook have been able to achieve this goal. But, with a seamless CI/CD pipeline, multiple daily releases can be made a reality.

Teams can build, test and deploy features automatically with almost no manual intervention. This is accomplished using various tools, frameworks, and systems like Travis CI, Docker, Kubernetes, and LaunchDarkly.

3. Expand less manual effort

To align with the shift-left paradigm, we need automation right from the start. This is also a vital component of having a successful CI/CD implementation. Once you build features and check in code, tests should be automatically triggered to make sure that the new code does not break existing features and that the new features are working correctly.

After the tests run, the code gets deployed to different environments, including QA, staging and production. Throughout this process, you will be getting constant notifications through different channels, giving you plenty of information about the build, test and deploy cycles.

4. Generate extensive logs

One key aspect of observability is logging information. Logs are a rich source of information to understand what is happening beneath the UI and study application behavior.

With a CI/CD pipeline, extensive logging information is generated in each stage of the development process. There are various tools available to analyze these logs effectively and get immediate feedback about the system.


5. Make easier rollbacks

One of the biggest advantages of a CI/CD pipeline is you can roll back changes quickly. If any new code changes break the production application, you can immediately return the application to its previous state. Usually, the last successful build gets immediately deployed to prevent production outages.

## What are the other tools available for CICD pipeline - Why Jenkins?

- Jenkins is designed to handle anything from a simple CI server to a complete CD hub.

- Spinnaker, a CD platform built for multicloud environments.

- GoCD, a CI/CD server with an emphasis on modeling and visualization.

- Concourse, "an open-source continuous thing-doer."

- Screwdriver, a build platform designed for CD.

- GitLab

- CircleCI

- Travis CL

- Atlassian Bamboo
-  <img width="1013" alt="Screenshot 2022-06-16 at 11 55 30" src="https://user-images.githubusercontent.com/105854053/174055492-c55ef424-3955-403b-97f2-168d7182f10f.png">


# Plan
- Generate ssh key pair on localhost in .ssh folder
- Copy the 114 114.pub key to our github
- Test the ssh connection 


## SSH Keys GitHub

Inside .ssh folder
1. ssh-keygen -t ed25519 -C "your_email@example.com"
2. eval "$(ssh-agent -s)"
3. ssh-add ~/.ssh/KEY NAME

Public key on GitHub
Private key on Jenkins

pbcopy < public/privatekey 

Inside GitHub repository
1. Settings
2. Deploy keys 
3. Add deploy keys


https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

# Jenkins Steps

Step 1: New Item

Step 2: Enter an item name + freestyle project

Step 3: Discard old builds

Step 4: Max # of builds to keep - 3

Step 5: Build - Execute shell - command

Step 6: Build Post-Build Actions - Build other projects

Step 7: Build now - Console output

![My First Board (1)](https://user-images.githubusercontent.com/105854053/174122912-223e8975-413a-46ad-bb6f-56d62225bde7.jpg)


# How to create Webhook 

Step 1: Navigate to the settings of your repository and select Webhooks

Step 2: Add Webhooks

Step 3: In the payload URL add your jenkins URL

Step 4: Trigger "Just the push event"

Step 5: Press Add Webhook

Step 6: Navigate back to jenkins and in the configuration tick GitHub hook trigger for GITScm polling

# Jenkins - Dev Branch to Main branch if test pass

Step 1: Create a new dev branch locally

Step 2: Follow git commands to connect this to github

Step 3: Follow steps above to create new item

Step 4: Changed branches to build specifier from main to /dev

Step 5: Tick GitHub hook trigger for GITScm polling

Step 6: Tick Provide NodeJS Installation

Step 7: Build Execute Shell and insert the following

cd app
npm install
npm test

Step 8: Post-Build Action

<img width="949" alt="Screenshot 2022-06-17 at 15 56 29" src="https://user-images.githubusercontent.com/105854053/174324959-b40ba75a-9fcf-41d6-b19e-eae83131ddb6.png">

In order to test this worked, nano readme.md and add information.

Then check if jenkins runs a new job and if github is updated. 

If this is the case, then you have done this correctly. 

## Setup App through Jenkins on AWS instance

Plan Diagram

<img width="898" alt="Screenshot 2022-06-20 at 17 11 16" src="https://user-images.githubusercontent.com/105854053/174642844-19230e39-9b08-4550-bde2-81991d84674c.png">


Firstly, set up your EC instance using these security groups.
This will allow jenkins ssh. 
<img width="998" alt="Screenshot 2022-06-20 at 16 16 15" src="https://user-images.githubusercontent.com/105854053/174633155-e98f4398-3580-47e7-a303-025b455ff6ee.png">

Then move over to jenkins and start a new job following the steps below


<img width="805" alt="Screenshot 2022-06-20 at 16 10 44" src="https://user-images.githubusercontent.com/105854053/174632025-ef0f37c5-8036-4ad8-8d87-c093ba9efc3a.png">

<img width="775" alt="Screenshot 2022-06-20 at 16 12 09" src="https://user-images.githubusercontent.com/105854053/174632380-d55142f5-627d-49c0-baf4-fba42a7d4da6.png">

<img width="812" alt="Screenshot 2022-06-20 at 16 13 11" src="https://user-images.githubusercontent.com/105854053/174632442-12f129c1-8aa4-4326-bd4d-4705f00dc6c3.png">

<img width="798" alt="Screenshot 2022-06-20 at 16 13 28" src="https://user-images.githubusercontent.com/105854053/174632505-26069e0f-1d2c-43eb-bfed-71bf1595c9a8.png">

<img width="944" alt="Screenshot 2022-06-20 at 16 19 57" src="https://user-images.githubusercontent.com/105854053/174633909-1a99dde1-6a4a-41ee-9b28-41fe360cb47d.png">

The below are the commands:

#!/bin/bash

`scp -v -r -o StrictHostKeyChecking=no app/ 
ubuntu@54.217.28.201:/home/ubuntu/`

`ssh -A -o StrictHostKeyChecking=no ubuntu@54.217.28.201 <<EOF`

`sudo apt-get update -y`

`sudo apt-get upgrade -y`

`sudo apt-get install nginx -y`

`sudo systemctl start nginx`

`sudo systemctl enable nginx`

`sudo systemctl status nginx`

`curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`

`sudo apt-get install -y nodejs`

`sudo npm install pm2 -g`

`sudo apt-get install python-software-properties -y`

`sudo cp default /etc/nginx/sites-available`
 
`sudo nginx -t`

`sudo systemctl restart nginx`

`sudo systemctl enable nginx`

This last step has to be done manually.

cd app/app
`npm install`

`nohup node app.js > /dev/null 2>&1 &`

![Screenshot_(176)](https://user-images.githubusercontent.com/105854053/174642947-2729d0f3-96ea-402a-90a6-dbba08323482.png)


                                                        
                                                              
                                                              
