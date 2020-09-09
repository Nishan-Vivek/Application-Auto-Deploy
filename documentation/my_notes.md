# Tasks

## Current

- Deploy phase []
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
  - verify test-build-deploy jobs together in workflow []
    - determine order [x]
    - link and test []
      - test backend wwith built files again [x]
      - test backend with source files again [x]
        - test front with front end [x]
        - build source workaround into workflow for now []
        - post on udacity []



## Done

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

## misc
aws ec2 describe-instances --filters "Name=tag-value,Values=backend-deployment-b359765" --query "Reservations[*].Instances[*].[PublicDnsName]" --output text
          
          curl -H "Content-Type: text/plain" -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request PUT --data "`cat /tmp/workspace/backend_url.txt`" https://api.memstash.io/values/blarf

curl -H "token: 170176fc-6ea1-4342-8d18-add32ecf9409" --request GET https://api.memstash.io/values/blarf

https://www.mydailytutorials.com/working-with-environment%E2%80%8B-variables-in-ansible/
https://stackoverflow.com/questions/27733511/how-to-set-linux-environment-variables-with-ansible

circleci working dir `/home/circleci/project/`

## scripts to set a batch of environment varibles
if using a bashscript to set environment variable for later use eg. `export myvar=value`. call the script using `.` or `source` eg `. myscript` this 
calls the script in the context of the calling shell. 
more info: https://stackoverflow.com/questions/16618071/can-i-export-a-variable-to-the-environment-from-a-bash-script-without-sourcing-i



## scratch

aws cloudformation list-exports --query "Exports[?Name==\`PipelineID\`].Value" --no-paginate


#### error when running built backend
```
ubuntu@ip-172-31-8-37:~$ cd web
ubuntu@ip-172-31-8-37:~/web$ ls
main.d.ts      main.hmr.js.map  migrations    package-lock.json
main.hmr.d.ts  main.js          modules       package.json
main.hmr.js    main.js.map      node_modules
ubuntu@ip-172-31-8-37:~/web$ node main.js
info: NodeJs Version v10.19.0
info: {"SHELL":"/bin/bash","TYPEORM_PASSWORD":"REDACTED","TYPEORM_USERNAME":"postgres","PWD":"/home/ubuntu/web","LOGNAME":"ubuntu","XDG_SESSION_TYPE":"tty","MOTD_SHOWN":"pam","HOME":"/home/ubuntu","TYPEORM_PORT":"5432","LANG":"C.UTF-8","LS_COLORS":"rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:","TYPEORM_HOST":"udacity.cwkvtnx7r2rh.us-west-2.rds.amazonaws.com","SSH_CONNECTION":"23.16.118.62 38126 172.31.8.37 22","LESSCLOSE":"/usr/bin/lesspipe %s %s","XDG_SESSION_CLASS":"user","TERM":"xterm-256color","LESSOPEN":"| /usr/bin/lesspipe %s","TYPEORM_CONNECTION":"postgres","USER":"ubuntu","TYPEORM_DATABASE":"mydatabase","ENVIRONMENT":"production","SHLVL":"1","XDG_SESSION_ID":"14","XDG_RUNTIME_DIR":"/run/user/1000","SSH_CLIENT":"23.16.118.62 38126 22","XDG_DATA_DIRS":"/usr/local/share:/usr/share:/var/lib/snapd/desktop","PATH":"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin","DBUS_SESSION_BUS_ADDRESS":"unix:path=/run/user/1000/bus","SSH_TTY":"/dev/pts/0","TYPEORM_ENTITIES":"./src/modules/domain/**/*.entity.ts","_":"/usr/bin/node","OLDPWD":"/home/ubuntu"}
debug: Starting Nest application...
debug: StatusModule dependencies initialized
debug: ConfigModule dependencies initialized
debug: TypeOrmModule dependencies initialized
debug: PassportModule dependencies initialized
debug: AuthModule dependencies initialized
debug: AppModule dependencies initialized
debug: CqrsModule dependencies initialized
debug: CommonModule dependencies initialized
debug: TypeOrmCoreModule dependencies initialized
error: No repository for "Product" was found. Looks like this entity is not registered in current "default" connection? {"trace":"RepositoryNotFoundError: No repository for \"Product\" was found. Looks like this entity is not registered in current \"default\" connection?\n    at new RepositoryNotFoundError (/home/ubuntu/web/node_modules/typeorm/error/RepositoryNotFoundError.js:11:28)\n    at EntityManager.getRepository (/home/ubuntu/web/node_modules/typeorm/entity-manager/EntityManager.js:670:19)\n    at Connection.getRepository (/home/ubuntu/web/node_modules/typeorm/connection/Connection.js:344:29)\n    at InstanceWrapper.useFactory [as metatype] (/home/ubuntu/web/node_modules/@nestjs/typeorm/dist/typeorm.providers.js:15:30)\n    at Injector.instantiateClass (/home/ubuntu/web/node_modules/@nestjs/core/injector/injector.js:291:55)\n    at callback (/home/ubuntu/web/node_modules/@nestjs/core/injector/injector.js:75:41)\n    at process._tickCallback (internal/process/next_tick.js:68:7)","context":"ExceptionHandler"}
```

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
arn:aws:s3:::udapeople-deployment-5455eb4
aws s3api list-buckets --output text | grep udapeople-frontend | awk '{ print $3 }'