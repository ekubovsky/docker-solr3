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

