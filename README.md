# mlflow



* Reference:
    * official website: https://mlflow.org/
    * github: https://github.com/mlflow/mlflow


## Installing docker/docker-compose
```sh
sudo amazon-linux-extras install docker
sudo service docker start
sudo chkconfig docker on
sudo usermod -a -G docker ec2-user
sudo usermod -a -G docker ssm-user
sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose version
```

## Usage
```sh
wget https://gist.githubusercontent.com/richardsonlima/cac79be243bff8d85ecaae993da3dfb1/raw/480a7fe6a0e5cfa88725d6f68f89a6f0838ce9a5/docker-compose.yaml
sudo docker-compose up -d
```

### Build a Docker image

```sh
git clone https://github.com/richardsonlima/mlflow-basis.git
cd ./mlflow-basis
sudo docker build -t mlflow-basis:latest .
```



### Run a Container

```sh
# list available docker images
sudo docker images

# list running containers
sudo docker ps -a

# run the container
# container port 5000: mlflow server
# --rm: remove the container while exiting
# -i: interactive
# -t: terminal mode
# -v: path for host:container
#
# example: docker run -it --rm --name mlflow -p 5000:5000 mlflow:latest
#
sudo docker run -it --rm --name mlflow -p 5000:5000 -v <local>:<container> mlflow-basis:latest

# stop the container
sudo docker stop mlflow

# restart the container
sudo docker restart mlflow

# remove the container
sudo docker rm mlflow
```



### Interact with Container

```sh
sudo docker exec -it mlflow /bin/bash
```



### mlflow Quickstart

* start the training in mlflow example

```sh
# by default
# working dir: /app/mlflow/examples
python ./quickstart/mlflow_tracking.py
```

* start the mlflow server to monitor the result

```sh
# host 0.0.0.0: allow all remote access
mlflow server --file-store ./mlruns --host 0.0.0.0
```



### Push to Dockerhub

```sh
sudo docker login

# set another tag
sudo docker tag mlflow-basis:latest <username_in_dockerhub>/mlflow-basis:<version>

# push to the dockerhub
sudo docker push <username_in_dockerhub>/mlflow-basis:<version>
```

