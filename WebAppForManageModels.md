
# A Web Application for Managing ML Models in Docker

## Build a platform for Manage & Run ML models & data

### Use Case

* ML Model Experts:
  ->Build Model with common libraries & platform 
      -> Train 
          -> Validate & Test 
              -> Wrapper in Docker Image 
                  -> Upload to Docker Repo for release

* Web Framework Server Developers:
  ->Pull all docker Images from Docker Repo
      -> Show docker image & description on the Web Page 
          -> Provide input parameter form based on Json Schema in docker image 
              -> Upload & Manage Dataset
                  -> Run dockers with data & parameters
                      -> Pull log & generated data & clean docker containers

 * Model Users:
  -> Browser models in Web Server
      -> Upload/Select dataset & configure parameter for selected model
          -> Run model by the Web Server
              -> View Model Results by the Web Server

* Model/Web Administrators:
  -> Evaluate models based on models' result
      -> Request Model experts to fine-tune model with new data if model result deteriorate 

### Design Thoughts
* Seperate of Concerns
* Platform Independent
* Same for edge & cloud

### Main Open Source libraries 
* Docker SDK for Python
https://docker-py.readthedocs.io/en/stable/client.html
https://github.com/docker/docker-py
* TensorFlow Docker Image for building ML model:
https://hub.docker.com/r/tensorflow/tensorflow/
