[![CircleCI](https://dl.circleci.com/status-badge/img/gh/guid1111/DevOps_Microservices/tree/develop.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/guid1111/DevOps_Microservices/tree/develop)


## Project Summary

House price prediction model.
This application will listen on port 80 for requests
JSON Requests can be sent using HTTP POST to the "/predict" endpoint.  The attributions of ths JSON payload should include a simple document with attributes such as number of rooms in a home, highway access etc.
The end point will output a single number containing the house price prediction.

## Instructions

The most repeatable way to build and run the application is to build a docker container for the application and run the container.
This can be done by running the script: ./run_docker.sh

If you wish to run the application locally, outside of the container you will require python3.7 (And if necessary use 3.7 for the virtual environment by using "virtualenv -p /usr/bin/python3.7 ~/.devops") and follow these steps:

- Create a python virtual environment by running: "make setup"
- After this run: "source ~/.devops/bin/activate" in a bash shell in order to start the virtual environment.
- Then run "make install" to install the application's dependencies in to your virtual python environment.
- And then you can run the application by running: "python3 app.py"
- To exit from the virtual environment run: "deactivate"


# Key Files
- .circleci/config.yml - configuration file for the circleci pipeline.  steps include invoking the lint makefile target.
- model_data folder - data for the prediction model.
- output_text_files/docker_out.txt - example output that will be seen when running the web application within a docker container, and submitting an HTTP request to make a prediction.
- output_text_files/kubernates_out.txt - similar to docker_out.txt, but output when running in a kubernates cluster, with details of the pod name and port forwarding.
- app.py - main file for the python application.
- Dockerfile - configuration file to build a docker container for the application, adding application and its dependencies to python:3.7.3 base image.  The image will be tagged with GitHubUser/ml-microservice
- make_prediction.sh - smoke test script to run that will call the running application on port 80, posting some data in order to get a house price prediction in the response.
- Makefile - targets include installing the environment dependencies in preparation for running, testing, and linting the python code and docker configuration files.
- requirements.txt - list of python packages required for the application to run.  Used for the makefile and when building the docker container.
- run_docker.sh - script to run to build and run the docker container.  Requests on port 80 will be forwarded to port 8000 where the container is listening.
- run_kubernates.sh - script to run a kubernates cluster using the docker image of this application pulled from docker hub.  Requests on port 80 will be forwarded to port 8000 where the container is listening.
- upload_docker.sh - script to upload the docker image previously built and tagged GitHubUser/ml-microservice to docker hub.