# Check You Self Local Development Environment

This repository is all about showing what it takes to create a local
docker-compose environment in which all our services can run in harmony.

I like to use docker-compose environments to mimic what it will be like
for my containers to run in a Kubernetes cloud environment. If everything runs
well in my local docker-compose network, everything really should be mostly
fine in the cloud.

There are three parts to this repo. There is a docker-compose file that brings
up the infrastructure pieces our app needs. It creates a MySql and Adminer instance,
and it brings up Elasticsearch and Kibana.

There is a docker-compose file that contains the services I wrote. This includes
the check-yo-self frontend, the indexer service, and the API. It also includes
a bootstrapper container that sets things up nicely for us as the compose
network comes to life.

Finally, I've included example Kubernetes yaml files that could be used
to bring up the API and the frontend in Kubernetes. But don't get me wrong.
There's really nothing in this repo related directly to Kubernetes. I'm just
pointing you in the direction of your next steps should you want to deploy
your container to Kubernetes.

## Directions for Getting Everything Running

### Create all Your Containers

First, you'll need to visit the other repos related to this project, and you'll
follow the instructions in each repo regarding how to create a Docker container
image for that project. Those projects are:

* check-yo-self
* check-yo-self-indexer
* check-yo-self-api
* check-yo-self-bootstrapper

### Run the Infrastruction docker-compose

Now, we need to get our infrastructure running. To do that, just change directories
into the Infrastructure folder, and run the following command:

```bash
docker-compose up -d
```

This will bring up MySql, Adminer, Elasticsearch, and Kibana. Please note
that I've volumed the data from MySql and Elasticsearch to the Infrastructure
folder. So when you start the services up, you'll notice an elasticsearchData
and a mySqlData folder appear in the Infrastructure folder. To clear the data
for subsequent runs of the docker-compose, simply delete these volume folders
prior to running docker-compose up.

### Run the Application docker-compose

Now, we'll start up the services in this project. To do that, just change directories
into the Application folder, and run the following command:

```bash
docker-compose up -d
```

This docker-compose file uses the docker-compose network that was created
when we started up the infrastructure above. That means our services can
freely communicate with the infrastructure services by default. No coding.
No configuring.

### Looking at the App

Once everything is running, simply browse to [http://localhost:5000](http://localhost:5000).
There you'll find check-yo-self running like a champ!!
