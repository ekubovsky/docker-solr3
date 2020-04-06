# docker-solr3

Solr 3.x Docker image  
Inspired by https://github.com/docksal/service-solr

## Build instructions

1. Obtain this Docker Solr3 image from **https://github.com/ekubovsky/docker-solr3/archive/master.zip**
2. Unzip and build the image: ```docker build . -t <TAG>```
3. Run image:
   - Detached, with exposed port: ```docker run -d -p 8983:8983 --name solr3 <TAG>```
   - Detached, with exposed port and shared folder ```docker run -d -v <host/path>:</mount/path> -p 8983:8983 --name solr3 <TAG>```
4. Run a command inside the container: ```docker exec -ti -w /opt/solr/example Solr3 "COMMAND"```

Solr will be availavle on ```http://1287.0.0.1:8983/sorl```

## Image details

This configuration implies running a single core. Solr directories in the container:
* conf path: ```/var/lib/solr/conf```
* data volume: ```/var/lib/solr/data```

## Solr configuration

Several config options are available for this image in the ```src``` folder:
* ```src/default```: somewhat default Solr configs
* ```src/drupal-apachesolr```: configuration shipped along Drupal contrib Apache Solr module

Copy desired configuration into ```conf``` folder before buildin an image.

## Persistent Local Volumes

If you wish to create named local volumes that persist in the location(s) you want - install [local-persist Docker plugin](https://github.com/Matchbooklab/local-persist). Now create a volume using the driver provided by this plugin. The example below mounts a volume on local ```conf``` folder (empty by default):

```docker volume create -d local-persist -o mountpoint=$PWD/conf --name=solr-conf```

Before you run/create a containr, copy your Solr configuration files into mounted folder from above, and then run/create your container using ```-v``` option:

```docker run -d -v solr-conf:/var/lib/solr/conf Solr3```

As a result you will have a shared configuration folder, available for both the host and the container. Keep in mind, that Solr 3 does not suport restarting the Solr server - in order for your configuration changes to take effect you will have to kill the process and start Solr conrainer again. The index data should be persisten, as per Dockerfile specification.



