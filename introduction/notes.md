
## run docker 
What docker is, why we need it
Running postgres locally with docker
Putting some data for testing to local postgres with Python
Packaging this script in docker
Running postgres and the script in one network
Docker compose and running pgadmin and postres together with docker-compose
SQL: group by, joins, window function, union

## Docker

Docker allows you to put everything an application needs inside a container - sort of a box that contains everything: OS, system-level libraries, python, etc.
You run this box on a host machine. The container is completely isolated from the host machine env.
In the container you can have Ubuntu 18.04, while your host is running on Windows.
You can run multiple containers on one host and they won’t have any conflict.
An image = set of instructions that were executed + state. All saved in “image”
Installing docker: https://docs.docker.com/get-docker/

Why should data engineers care about containerization and docker?

- Setting up things locally for experiments
- Integration tests, CI/CD
- Batch jobs (AWS Batch, Kubernetes jobs, etc — outside of the scope)
- Spark
- Serverless (AWS Lambda)
- So containers are everywhere

Simple example

- Python 3.9
- Extend it - install some libraries like pandas
- More - next




Try this code to run the image ubuntu
``` docker run -it ubuntu bash``
Experiment with socker by running the python image with the tag or version 3.9
```docker run -it python:3.9  ```

restart your docker on MacOs

``` docker-machine restart```

Let's install pandas in our docker image.
To be able to get to bash we need to include the entry point into our commmand.
```docker run -it --entrypoint=bash python:3.9 ```

you need to be in the directory where docker is. To install pandas
type ```pip install pandas```

If our image doebt have all required packages, once we leave the bash where we installed the package we loose all installed packages when we type our entry point ```docker run -it --entrypoint=bash python:3.9 ``` code again. This image will show the initial packages. It is advised to have a dokerfile.

``` FROM python:3.9

RUN pip install pandas

ENTRYPOINT ["bash"]
```

Then type ``` docker build  -t test:pandas .``` For example test pandas with a . to create an image in this directory.