# Working with travis & docker

Travis is a CI/CD tool that works with docker. Any time changes are being done, travis detects them, runs test and pushes them to cloud (AWS).


## Travis understanding

File: `.travis.yml`

```yml
sudo: required              # sudo access is mostly requried
services: 
    - docker                # installs a copy of docker ready to go.

before_install:
    - docker build -f -t <docker_username>/<cotaniner_name> <Dockerfile.dev> . 
    # runs before deploying, or final processes.
    # builds a container from a Dockerfile

script:                     # commands to run tests/deployment.
    - docker run <container_id> <sample_code>
    # runs docker scripts inside the container.

deploy:                     # take stuff and deploy our project
    provider: elasticbeanstalk
    # cloud service provider

    region: 
    # region of the ElasticBeanTalk instance.

    app: 
    # name of the app  <app_name> on the the cloud platform

    env:
    # name of the environment.

    bucket_name:
    # S3 bucket. (Give Elastic BeansTalk access the files from S3)

    bucket_path:
    # path for the project. <app_name> by default.

    on:
    # auto deploy on pushes to what place.
        branch: master 
        # master by default

    access_key_id:
    # ACCESS KEY ID

    secret_access_key:
    # SECRET ACCESS KEY
    

```

## AWS with Travis & Docker

For CI/CD with AWS\.

Amazon Elastic Beanstalk handles continues deployment.

