# Notes

Starter files are not finalized :-( Keep an eye and merge as needed. 
https://github.com/udacity/cdond-c3-projectstarter
git pull https://github.com/udacity/cdond-c3-projectstarter.git master

## Local CircleCI

Issues running CircleCI locally following recommended install method (snap).
Manual install + docker from docker repo works. Did not test with docker from ubuntu repos.
circleci config process .circleci/config.yml > local.yml
circleci local execute -c local.yml --job JOB_NAME



