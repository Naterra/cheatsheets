In software engineering, CI/CD or CICD generally refers to the combined practices of continuous integration and either continuous delivery or continuous deployment. CI/CD bridges the gaps between development and operation activities and teams by enforcing automation in building, testing and deployment of applications.


Continuous integration (CI) and continuous delivery (CD) embody a culture, set of operating principles, and collection of practices that enable application development teams to deliver code changes more frequently and reliably. The implementation is also known as the CI/CD pipeline

CI/CD is one of the best practices for devops teams to implement. It is also an agile methodology best practice, as it enables software development teams to focus on meeting business requirements, code quality, and security because deployment steps are automated.

Continuous integration is a coding philosophy and set of practices that drive development teams to implement small changes and check in code to version control repositories frequently. Because most modern applications require developing code in different platforms and tools, the team needs a mechanism to integrate and validate its changes.


**Continuous Integration(CI)** — is a development practice where developers integrate code into a shared repository frequently, preferably several times a day. Each integration can then be verified by an automated build and automated tests.

**Continuous Deployment(CD)** — is a strategy for software releases wherein any code commit that passes the automated testing phase is automatically released into the production environment, making changes that are visible to the software’s users.


**Continuous Integration (CI)** is the practice of testing the application on each update. Doing this manually is tedious and error-prone, but a CI platform runs the tests for you, catches errors early, and locates the point at which the errors were introduced. Release and deployment procedures are often complicated, time-consuming, and require a reliable build environment.

With **Continuous Delivery (CD)** you can build and deploy your application on each update without human intervention.



<img width='600' src='https://solidstudio.io/img/blog/cd/pipeline.png?ver=1'/>

Jenkins - 
Docker - 

### Pipes(integrations)
Pipes provide a simple way to configure a pipeline. You can add as many pipes as you like.

A pipe is a custom Docker image for a container, which contains a script to perform a task.

```javascript
script:
  - pipe: atlassian/aws-s3-deploy:0.2.2
    variables:
      AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID
      AWS_SECRET_ACCESS_KEY: $AWS_SECRET_ACCESS_KEY
      AWS_DEFAULT_REGION: 'us-east-1'
      S3_BUCKET: 'my-bucket-name'
      LOCAL_PATH: 'build'
```


### Pipelines

```javascript
#  root/bitbucket-pipelines.yml
#  Template NodeJS build

#  This template allows you to validate your NodeJS code.
#  The workflow allows running tests and code linting on the default branch.

image: node:10.15.3

pipelines:
  default:
    - parallel:
        - step:
            name: Build and Test
            caches:
              - node
            script:
              - npm install
              - npm test
        - step:
            name: Code linting
            script:
              - npm install eslint
              - npx eslint .
            caches:
              - node
```






## Example 2 -   deployment with Docker
1. Whenever a new commit is made (to any branch), we install npm packages and run tests.
2. When a new commit is made to master branch, we execute 2 steps.



```javascript
pipelines:
  default:
  - step:
      name: Build and Test
      image: node:10.15.0
      caches:
      - node
      script:
      - npm install
      - npm test

  branches:
    master:
    - step:
        name: Deploy to Registry
        script:
        - export IMAGE_NAME=your_name/project_name:$BITBUCKET_COMMIT
        - docker build -t $IMAGE_NAME .
        - docker login --username $DOCKER_HUB_USERNAME --password $DOCKER_HUB_PASSWORD
        - docker push $IMAGE_NAME
        
    - step:
        name: Deploy to droplet
        script:
        - export IMAGE_NAME=your_name/project_name:$BITBUCKET_COMMIT
        - pipe: atlassian/ssh-run:0.2.2
          variables:
            SSH_USER: $SSH_USER
            SERVER: $SSH_SERVER
            COMMAND: >
              docker stop $CONTAINERS_TO_STOP
              docker run -p $SERVER_PORT:$SERVER_PORT -d  $IMAGE_NAME
        services:
        - docker
```


### Deployment via SSH and shell

```javascript
  branches:
    master:
    - step:
      name: deploy to production
      #deployment: test
      script:    
        - echo "Deploying master to live"
        - pipe: atlassian/ssh-run:0.1.4
          variables:
            SSH_USER: '{sshuser}'
            SERVER: '{serverip}'
            COMMAND: 'ci-scripts/pull-deploy-master.sh'
            MODE: 'script'
```


### Deployment via hmmm...
https://stackoverflow.com/questions/63186156/how-to-deploy-react-app-in-ubuntu-server-with-bitbucket-pipeline
```javascript
default:
    - step:
        name: Build React Project
        script:
            - npm install
            - npm run-script build
            - mkdir packaged
            - tar -czvf packaged/package-${BITBUCKET_BUILD_NUMBER}.tar.gz -C build .
        artifacts:
            - packaged/**
    - step:
        name: Deploy to Web
        image: atlassian/default-image:latest
        trigger: manual
        deployment: production
        script:
            - mkdir upload
            - tar -xf packaged/package-${BITBUCKET_BUILD_NUMBER}.tar.gz -C upload
            - rsync -a --delete upload/ $USERNAME@$SERVER:/home/temp/react-${BITBUCKET_BUILD_NUMBER}
            - ssh $USERNAME@$SERVER "rm -r /home/www"
            - ssh $USERNAME@$SERVER "mv '/home/temp/react-${BITBUCKET_BUILD_NUMBER}' '/home/www'"
            - ssh $USERNAME@$SERVER "chmod -R u +rwX,go+rX,go-w /home/www"
        artifacts:
            - upload/**
```


### Via SSH???
```javascript
ssh codeship_user@your.droplet.com \
'cd ~/src/repo ; systemctl stop node-sample ; git pull ; systemctl restart node-sample'
```



### Resources
- [CI/CD Explained, + Jenkins](https://www.youtube.com/watch?v=m0a2CzgLNsc)

- [What are Pipes](https://support.atlassian.com/bitbucket-cloud/docs/what-are-pipes/)
- [Get Started With Bitbucket Pipelines](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/)
- [Deploy your application to Digital Ocean using Docker and Bitbucket Pipelines](https://medium.com/@barfiagyenim/deploy-your-application-to-digital-ocean-using-docker-and-bitbucket-pipelines-cf4eb8eaaa0d)
 
 
 
 
  https://stackoverflow.com/questions/57364729/deploy-with-bitbucket-pipelines-nodejs-application-to-vps
  https://medium.com/@barfiagyenim/deploy-your-application-to-digital-ocean-using-docker-and-bitbucket-pipelines-cf4eb8eaaa0d#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6ImZlZDgwZmVjNTZkYjk5MjMzZDRiNGY2MGZiYWZkYmFlYjkxODZjNzMiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJuYmYiOjE2MTQyNzAxMjQsImF1ZCI6IjIxNjI5NjAzNTgzNC1rMWs2cWUwNjBzMnRwMmEyamFtNGxqZGNtczAwc3R0Zy5hcHBzLmdvb2dsZXVzZXJjb250ZW50LmNvbSIsInN1YiI6IjEwODkwOTUyOTQ1Mjc4Mzk3OTI4OSIsImVtYWlsIjoibmF0YWxpbnl3ZWJAZ21haWwuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImF6cCI6IjIxNjI5NjAzNTgzNC1rMWs2cWUwNjBzMnRwMmEyamFtNGxqZGNtczAwc3R0Zy5hcHBzLmdvb2dsZXVzZXJjb250ZW50LmNvbSIsIm5hbWUiOiJOYXRhbGkgQiIsInBpY3R1cmUiOiJodHRwczovL2xoMy5nb29nbGV1c2VyY29udGVudC5jb20vYS0vQU9oMTRHaHlPUDZmSUdkcnVFSTZYRmlFNEpoTXdVeW9rOFgxYXVRSjZMOVBpZz1zOTYtYyIsImdpdmVuX25hbWUiOiJOYXRhbGkiLCJmYW1pbHlfbmFtZSI6IkIiLCJpYXQiOjE2MTQyNzA0MjQsImV4cCI6MTYxNDI3NDAyNCwianRpIjoiYTE4MDBlZTlhYTc3MThiYmU0NDVkNjgxYTE2NDMyM2JkYWZkOWI1OSJ9.df_1oNyVrZQ_nknipf2BBe0JKy5hNyPa3E9XhPvE0QZC1U0_JNJZI-53n6dvbRQBhB0-jzh0V-SUinJa5A_dQwdzcKbSppS7h3azYzH551ABh1zGiKqNVpZvwemItNZa5immi6M1UGFH9xBQwmeZ-zWhXnJkuRAGSbf-SnXOogVe69hL8eYhmCO9qOdewtpnMAQWv9fzzR09mYoh_41dAolnkTGd8BfOH0wCSYPeqdOmxuQhGcSTz6WiPSDBWLXlBV7WEKudC6Nn0T1BPIrtJ6FUEM2-t6QVCrtYsyi60zb1RWByBu5uwmFaqpFlpybiZfGSplZsU5IAFHpsSAerxQ
 
https://andela.com/insights/continuous-deploymentcd-using-bitbucket-pipelines-and-ubuntu-server/
http://alexnj.com/blog/continuous-deployment-of-node-js-application-to-digitalocean-using-semaphore-ci/
http://blog.shippable.com/continuous-deployment-to-digital-ocean-for-nodejs-app
https://support.atlassian.com/bitbucket-cloud/docs/write-a-pipe-for-bitbucket-pipelines/
https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/
https://www.infoworld.com/article/3271126/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html

https://community.atlassian.com/t5/Bitbucket-Pipelines-questions/Bitbucket-pipeline-to-deploy-code-to-DigitalOcean/qaq-p/1096834

node app digitalocean bitbucket pipe


The commands you are defining under script are going to be run into a Docker container and not on your VPS.
