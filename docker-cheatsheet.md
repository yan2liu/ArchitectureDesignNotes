# docker - docker cheatsheet

# cleanup
## Prune the system: all stopped containers, unused volumes, network, dangling images

//prune the system https://docs.docker.com/engine/reference/commandline/system_prune/:
	$ docker system prune
  
## delete volumes

    // see: https://github.com/chadoe/docker-cleanup-volumes
    
    $ docker volume rm $(docker volume ls -qf dangling=true)
    $ docker volume ls -qf dangling=true | xargs -r docker volume rm
    
## delete networks

    prune the networks https://docs.docker.com/engine/reference/commandline/network_prune/:
	$ docker network prune
    
## remove docker images
    
    // see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images
    
    $ docker images
    $ docker rmi $(docker images --filter "dangling=true" -q --no-trunc)
    
    $ docker images | grep "none"
    $ docker rmi $(docker images | grep "none" | awk '/ / { print $3 }')

## remove docker containers

    // see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images
    
    $ docker ps
    $ docker ps -a
    $ docker rm $(docker ps -qa --no-trunc --filter "status=exited")
    
## Resize disk space for docker vm
    
    $ docker-machine create --driver virtualbox --virtualbox-disk-size "40000" default
    
# Query
## find docker image with repository name matching pattern: */*/AAA*'
   $ docker images --filter=reference='*/*/AAA*'
