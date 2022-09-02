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


after_success:
    - docker build -t <docker_id>/<image_name> <path>
    # build container from docker file

    - docker login -u <docker_id>  --password-stdin (take password from STDIN)
    # Log in to docker CLI

    - docker push <docker_id>/<image_name>
    # push images to docker hub
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

For multicontainer projects use:

`Dockerrun.aws.json` - Container definitions, and build images from docker hub. [AWS Task definition reference](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#container_definitions)


Dockerrrun.aws.json:

```json
{
    "AWSEBDockerrunVersion": '2',      // version of interpretation,
    "containerDefinitions": [
        {
            "name": // name of service, could be anything
            "image": <docker_id>/<container_name> // docker image to use
            "hostname": // name of host service
            "essential": true/false // atleast 1 service in json has to be essential.
            "portMappings": [
                {
                    "hostPort": <port_id>,
                    "containerPort": <port_id>
                }
            ],
            "links": // allows containers to communicate with each other without need for port mapping./
            "memory": numeric // memory allocation for deployment.
        }
    ]
}
```