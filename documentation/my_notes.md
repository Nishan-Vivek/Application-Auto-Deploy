# Tasks

## Current
 - S3 bucks creation and saving of old and current ARNS []
  - create new s3 bucket [x]
  - ensure old s3 bucket arn is saved []    
      - get previous bucket arn []
          `echo "arn:aws:s3:::`aws s3 ls | awk '{ print $3 } ' | grep udapeople-deployment`" >> old_s3arn.txt`
      - save previous bucket arn to workspace []
## Done

- Backend infra creation and app deployment [x]
    - SPin up backend instance. [x]
    - Start creating ansible playbook to run from local as per requirements up till pm2 install. and test from worksation. [x]
    - setup local vars to match circleci vars. Put in a script for easy use. [x]
    - follow tutorial to pull env vars from workstation into playbook and print. [x]
    - now that vars are being printed from ansible. Run from circle ci to make sure circli environment varible are being seen. [x]
    - set test variable on host as per other link [x]
    - use asible to set required environment variables on backend server [x]
    - test PM2 running a test node app and get it to work as a service [x]
    - test current workflow on brand new instance [x]
    - have inventory file generated automatically and used in workflow [x]
    
    - package and deploy actual backend application [x]
        - looks like there are depenency issues, worked around by copying package.json and running npm i. This doesn't sound right so will post question 
        when channel available. 
    - test with db down and up and compare logs to ensure db connection now works [x]
    - clean up and merge when backend server ansible done []



# Notes

Starter files are not finalized :-( Keep an eye and merge as needed.   
https://github.com/udacity/cdond-c3-projectstarter  
git pull https://github.com/udacity/cdond-c3-projectstarter.git master

## Local CircleCI

Issues running CircleCI locally following recommended install method (snap).
Manual install + docker from docker repo works. Did not test with docker from ubuntu repos.
circleci config process .circleci/config.yml > local.yml
circleci local execute -c process.yml --job JOB_NAME
Difference between running circleci cli locally and running remotely with test-frontend job. Required oauth-sign added to package.json to work on remote.

## Circleci Jest/Junit test reporting

Added jest-junit+reports to package.json for frontend to enable test reporting in circlci.

## branches and builds
Limited builds to master and feature branch. 

## misc
aws ec2 describe-instances --filters "Name=tag-value,Values=backend-deployment-b359765" --query "Reservations[*].Instances[*].[PublicDnsName]" --output text
          
          curl -H "Content-Type: text/plain" -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request PUT --data "`cat /tmp/workspace/backend_url.txt`" https://api.memstash.io/values/blarf

curl -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request GET https://api.memstash.io/values/blarf

https://www.mydailytutorials.com/working-with-environment%E2%80%8B-variables-in-ansible/
https://stackoverflow.com/questions/27733511/how-to-set-linux-environment-variables-with-ansible

## scripts to set a batch of environment varibles
if using a bashscript to set environment variable for later use eg. `export myvar=value`. call the script using `.` or `source` eg `. myscript` this 
calls the script in the context of the calling shell. 
more info: https://stackoverflow.com/questions/16618071/can-i-export-a-variable-to-the-environment-from-a-bash-script-without-sourcing-i



## scratch

aws cloudformation list-exports --query "Exports[?Name==\`PipelineID\`].Value" --no-paginate



### the following was added to the original circleci config.yml template, not worth merging

```yml
### It's a good practice to keep your commands at the top of the config file. In this project, you'll need at least 2 commands:

# commands:
#   destroy-environment:
#     description: Destroy backend and frontend cloudformation stacks given a workflow ID.
#     ...

#   revert-migration:
#     description: Revert the last migration if successfully run in the current workflow.
#     ...

jobs:
  hello-world: # Delete this job when you get started
    docker:
      - image: amazon/aws-cli
    steps:
      - checkout
      - run:
          name: Say Hello
          command: |
            echo "Hello World"
#  build-frontend:

#  build-frontend:

#  test-frontend:

#  est-backend:

#  can-frontend:

#  scan-backend:

#  deploy-infrastructure:

#  configure-infrastructure:

#  run-migrations:

#  deploy-frontend:

#  deploy-backend:  

#  smoke-test:

#  cloudfront-update:

workflows:
  default:
    jobs:
      - hello-world
```
arn:aws:s3:::udapeople-deployment-5455eb4