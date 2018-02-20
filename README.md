# ICS5114 Big Data Processing -- NoSQL Databases Workshop

During this workshop I will show you the basic concepts of NoSQL systems.  We 
will use four NoSQL technologies, each representing a different data model 
-- Memcached, MongoDB, Cassandra, and Neo4j.

## Requirements

The following assumes you have a base Linux (Ubuntu 16.04) installation.  If you 
are a windows fan, may I suggest you create a beefy VM (using VirtualBox or on 
the cloud) and install Ubuntu there.

You will need a ton of different software (configuration, etc.) for this workshop.
Normally, this would be a pain, but we will be using docker so everything is 
conveniently installed and set-up for you and placed in different docker 
containers (you're spoilt these days!).

The rest of the workshop (and practical) assumes you have docker installed.
This can be achieved readily (on Ubuntu 16.04.3 LTS) with:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
sudo systemctl status docker
sudo usermod -aG docker ${USER}
```

## NoSQL Database Engines

We will use (the latest) official docker instances to install the NoSQL database
engines.  Follow the instructions presented in each section.  Each of these steps
may take a few minutes.  All the names of the containers will be prefixed with
`some-`.

### Memcached

To run memcached execute:

```
docker run --init --name some-memcache -d memcached
```

`-d` detaches the docker container once initialized.

### MongoDB

To run mongodb execute:

```
docker run --name some-mongo -d mongo
```

### Cassandra

To run cassandra execute:

```
docker run --name some-cassandra -d cassandra
```

### Neo4J

To run neo4j execute:

```
docker run --name some-neo4j --env=NEO4J_AUTH=none -p=7474:7474 -p=7687:7687 -d neo4j
```

## Jupyter Lab 

I have developed example usages of each NoSQL database, using Jupyter lab.  This
is a browser-based IDE on Jupyter Notebooks.  First, you should copy **all** 
code (as Jupyter notebooks) [here](https://github.com/jp-uom/ARI5902_Research_Topics_In_Artificial_Intelligence/tree/master/jupyter) 
in a local directory on your Ubuntu installation.

```
docker run -ti --rm --name nosql-workshop -v /home/jp/cloud/google-drive-uom/lecturing/2017-2018/ICS5114_Big_Data_Processing/class_practicals/nosql/docker/jupyter:/notebooks --link some-memcache:memcache --link some-mongo:mongo --link some-cassandra:cassandra --link some-neo4j:neo4j -p=8888:8888 jpebe/nosql-workshop
```
You should then be able to copy the Jupyter notebook URL from the terminal into your browser (ctrl-click will open a browser automatically).


# Important Limitations

The databases we run with the container have no volume mounted.  This means that
all data created during our exercises are stored in the container which gets reset
when you reinitialize the container.  If you want your data to persist, you
have to mount volumes (on your Ubuntu installation) and use these as the data dir
of the NoSQL engine. 


<!--
```
docker pull jpebe/nosql
```
-->


<!--
```
docker run -ti --rm --name nosql-workshop -v /home/jp/cloud/google-drive-uom/lecturing/2017-2018/ICS5114_Big_Data_Processing/class_practicals/nosql/docker/jupyter:/notebooks --link some-memcache:memcache --link some-mongo:mongo --link some-cassandra:cassandra --link some-neo4j:neo4j -p=8888:8888 jpebe/nosql-workshop
```
-->

** Pull requests (with fixes) will be recieved with thanks. **

I hope you enjoy the session!

![](https://github.com/drmenguin/learnd/blob/master/jp.gif)
