# scratch
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE --query "StackSummaries[].[StackName]" --output text | grep backend | awk -F- '{print $2}'
udapeople-frontend-deployment-${CIRCLE_WORKFLOW_ID:0:7}
if curl -s ${URL} | grep "Wecome"; then return 0; else return 1 ; fi
aws cloudformation deploy --template-file cloudfront.yml --stack-name udapeople-cloudfront --parameter-overrides WorkflowID="frontend-deployment-nishanstarter"

if grep -F "has been executed successfully." ./output.txt; then echo "true"; else echo "false"; fi


aws cloudformation update-stack --use-previous-template --stack-name udapeople-cloudfront --parameters ParameterKey=WorkflowID,ParameterValue="frontend-deployment-${CIRCLE_WORKFLOW_ID:0:7}"

              aws cloudformation deploy --template-file /home/circleci/project/.circleci/files/cloudfront.yml --stack-name udapeople-cloudfront --parameter-overrides WorkflowID="frontend-deployment-${CIRCLE_WORKFLOW_ID:0:7}"

# Tasks

- Setup monitor and logging
  - setup prometheus server []
      - create instance [x]
      - install server software []
      - setup aws service discovery []
  - setup back-end monitoring []
  - setup alerts []
  -



- DEBUG why cloudfront cannot view or save employees even though it was switched []
 - delete current distribution after it has disabled [x]
 - start new distro [x]
 - Issue is related browser blocking mixed ssl, likely needs more involved work around like elb or adding cert to backend server will do later []



## Done

 - promote phase [x]
  - setup initial cloudfront and bucket [x]
  - promote job after passing smoke tests that redirects cloudfront to new bucket [x]
  - break out migration:revert from rollback.[x]
  - clean up old stacks on succesfuly promotion [x]

- test migration revert with forced true [x]
- capture failed smoke test screen shot from circleci [SCREENSHOT6]

- rollback phase [x]
  - front end roll back [x]
    - empty s3 bucket [x]
    - delete front end stack [x]
  - back end roll back [x]
    - delete stack [x]
    - roll back migrations
      - how to tell if migration was run [x]
      - how to roll back migration [x] 
  Provide a screenshot for a successful rollback after a failed smoke test. [SCREENSHOT07]


- Smoke test phase [x]
  - write and test front end smoke job [x]
    - test with manual url [x]
    - get url properly
  - write and test back end smoke job [x]
    - test manual url [x]


- Deploy phase [x]
  - where in workflow to run database migration
    - Job to run database migration [x]
    - save true/false if database mirgration was run [x]
  - Job to copy build backend files to ec2 backend [x]
  - rebuild backend files with api_url job [x]
    - ensure api url is saved and accesible [x]
    - does build [x]
    - build files saved [x]
  - deploy backend files to new s3 bucket [x]
    - copy tar to temp directory [x]
    - uncompress and verify [x]
    - add s3 bucket creation to workflow [x]
    - verify bucket name is saved and usable [x]
    - copy to s3 bucket [x]
    - verify bucket public and app visible [x]
  - verify test-build-deploy jobs together in workflow [x]

 - S3 bucks creation and saving of old and current ARNS [x]
    NOTE: Had to change bucket naming convention due to issue with undeletable old S3 buckets
  - create new s3 bucket [x]
  - ensure old s3 bucket arn is saved []    
      - get previous bucket arn []
          `echo "arn:aws:s3:::`aws s3 ls | awk '{ print $3 } ' | grep udapeople-deployment`" >> old_s3arn.txt`
      - save previous bucket arn to workspace [x]

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

## old scratch
aws ec2 describe-instances --filters "Name=tag-value,Values=backend-deployment-b359765" --query "Reservations[*].Instances[*].[PublicDnsName]" --output text
          
          curl -H "Content-Type: text/plain" -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request PUT --data "`cat /tmp/workspace/backend_url.txt`" https://api.memstash.io/values/blarf

curl -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request GET https://api.memstash.io/values/blarf

https://www.mydailytutorials.com/working-with-environment%E2%80%8B-variables-in-ansible/
https://stackoverflow.com/questions/27733511/how-to-set-linux-environment-variables-with-ansible

circleci working dir `/home/circleci/project/`

aws cloudformation list-exports --query "Exports[?Name==\`PipelineID\`].Value" --no-paginate

arn:aws:s3:::udapeople-deployment-5455eb4
aws s3api list-buckets --output text | grep udapeople-frontend | awk '{ print $3 }'

## scripts to set a batch of environment varibles
if using a bashscript to set environment variable for later use eg. `export myvar=value`. call the script using `.` or `source` eg `. myscript` this 
calls the script in the context of the calling shell. 
more info: https://stackoverflow.com/questions/16618071/can-i-export-a-variable-to-the-environment-from-a-bash-script-without-sourcing-i

## example dbmigration log output

### no migrations

```
> glee2@1.0.0 premigrations /home/circleci/project/backend
> npm run build


> glee2@1.0.0 build /home/circleci/project/backend
> tsc


> glee2@1.0.0 migrations /home/circleci/project/backend
> ts-node -r dotenv/config node_modules/.bin/typeorm migration:run

query: SELECT * FROM "information_schema"."tables" WHERE "table_schema" = current_schema() AND "table_name" = 'migrations'
query: SELECT * FROM "migrations" "migrations" ORDER BY "id" DESC
No migrations are pending
```
### with applied migrations

```


query: SELECT * FROM "information_schema"."tables" WHERE "table_schema" = current_schema() AND "table_name" = 'migrations'
query: CREATE TABLE "migrations" ("id" SERIAL NOT NULL, "timestamp" bigint NOT NULL, "name" character varying NOT NULL, CONSTRAINT "PK_8c82d7f526340ab734260ea46be" PRIMARY KEY ("id"))
query: SELECT * FROM "migrations" "migrations" ORDER BY "id" DESC
0 migrations are already loaded in the database.
3 migrations were found in the source code.
3 migrations are new migrations that needs to be executed.
query: START TRANSACTION
query: CREATE TABLE "product" ("id" SERIAL NOT NULL, "description" character varying NOT NULL, CONSTRAINT "PK_bebc9158e480b949565b4dc7a82" PRIMARY KEY ("id"))
query: CREATE TABLE "order" ("id" uuid NOT NULL, CONSTRAINT "PK_1031171c13130102495201e3e20" PRIMARY KEY ("id"))
query: CREATE TABLE "order_products_product" ("orderId" uuid NOT NULL, "productId" integer NOT NULL, CONSTRAINT "PK_59f5d41216418eba313ed3c7d7c" PRIMARY KEY ("orderId", "productId"))
query: ALTER TABLE "order_products_product" ADD CONSTRAINT "FK_1f9ea0b0e59e0d98ade4f2d5e99" FOREIGN KEY ("orderId") REFERENCES "order"("id") ON DELETE CASCADE
query: ALTER TABLE "order_products_product" ADD CONSTRAINT "FK_d6c66c08b9c7e84a1b657797dff" FOREIGN KEY ("productId") REFERENCES "product"("id") ON DELETE CASCADE
query: INSERT INTO "migrations"("timestamp", "name") VALUES ($1, $2) -- PARAMETERS: [1549375960026,"AddOrders1549375960026"]
Migration AddOrders1549375960026 has been executed successfully.
query: ALTER TABLE "order_products_product" DROP CONSTRAINT "FK_d6c66c08b9c7e84a1b657797dff"
query: ALTER TABLE "product" DROP CONSTRAINT "PK_bebc9158e480b949565b4dc7a82"
query: ALTER TABLE "product" DROP COLUMN "id"
query: ALTER TABLE "product" ADD "id" uuid NOT NULL DEFAULT uuid_generate_v4()
query: ALTER TABLE "product" ADD CONSTRAINT "PK_bebc9158e480b949565b4dc7a82" PRIMARY KEY ("id")
query: ALTER TABLE "order_products_product" DROP CONSTRAINT "PK_59f5d41216418eba313ed3c7d7c"
query: ALTER TABLE "order_products_product" ADD CONSTRAINT "PK_1f9ea0b0e59e0d98ade4f2d5e99" PRIMARY KEY ("orderId")
query: ALTER TABLE "order_products_product" DROP COLUMN "productId"
query: ALTER TABLE "order_products_product" ADD "productId" uuid NOT NULL
query: ALTER TABLE "order_products_product" DROP CONSTRAINT "PK_1f9ea0b0e59e0d98ade4f2d5e99"
query: ALTER TABLE "order_products_product" ADD CONSTRAINT "PK_59f5d41216418eba313ed3c7d7c" PRIMARY KEY ("orderId", "productId")
query: ALTER TABLE "order_products_product" ADD CONSTRAINT "FK_d6c66c08b9c7e84a1b657797dff" FOREIGN KEY ("productId") REFERENCES "product"("id") ON DELETE CASCADE
query: INSERT INTO "migrations"("timestamp", "name") VALUES ($1, $2) -- PARAMETERS: [1549398619849,"FixProductIdTable1549398619849"]
Migration FixProductIdTable1549398619849 has been executed successfully.
query: CREATE TABLE "employee" ("id" SERIAL NOT NULL, "firstName" character varying(100) NOT NULL, "middleName" character varying(100), "lastName" character varying(100) NOT NULL, "secondLastName" character varying(100), "displayName" character varying(100), "companyEmail" character varying(50) NOT NULL DEFAULT '', "personalEmail" character varying(50) DEFAULT '', "birthdate" TIMESTAMP, "startDate" TIMESTAMP NOT NULL, "address" character varying(200), "phoneNumber" character varying(100), "bankName" character varying(100), "accountNumber" character varying(100), "gender" character varying, "tags" json NOT NULL DEFAULT '{}', "country" character varying(100) NOT NULL, "region" character varying(100) NOT NULL, "city" character varying(100) NOT NULL, "effectiveDate" TIMESTAMP NOT NULL, "salary" numeric NOT NULL, "salaryType" character varying NOT NULL, "isActive" boolean NOT NULL DEFAULT true, "workingHoursPerWeek" integer NOT NULL DEFAULT 40, CONSTRAINT "PK_3c2bc72f03fd5abbbc5ac169498" PRIMARY KEY ("id"))
query: CREATE INDEX "IDX_1f9ea0b0e59e0d98ade4f2d5e9" ON "order_products_product" ("orderId") 
query: CREATE INDEX "IDX_d6c66c08b9c7e84a1b657797df" ON "order_products_product" ("productId") 
query: INSERT INTO "migrations"("timestamp", "name") VALUES ($1, $2) -- PARAMETERS: [1555722583168,"AddEmployee1555722583168"]
Migration AddEmployee1555722583168 has been executed successfully.
query: COMMIT

```

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
