<H1>FIX on restart loses all registries data except for auth </H1>h1

## Example configuration for [docker-registry-web](https://github.com/mkuchin/docker-registry-web)

#### Before start: install docker
  As standard procedure

#### How to run:
    
    curl -L https://github.com/konrad2415/docker-registry-UI/archive/refs/heads/master.zip | tar -xzv
    cd examples/nginx-auth-enabled/
    ./generate-keys.sh
    docker-compose up
    

#### Create test user:
![Creating user](https://github.com/konrad2415/docker-registry-UI/blob/master/images/create-test.gif)
                 
### Bug fixes
    In Order to be accessible the cli docker login from remote hosts 
    using IP /OR dns were modified all references to localhost by 192.168.171.97 on  
        - file nginx-auth-enabled/conf/registry/config.yml  
        - nginx-auth-enabled/conf/nginx/default.conf 
### Internal web app UI 
     The internal web app is hosted by a TOMCATv7 web server 
     The views are located at /var/lib/tomcat7/webapps/ROOT/WEB-INF/grails-app/views/
     
#### Push some images

    docker login <hostIP/ORdns>:5000
    docker images 
    docker tag <localImage>:<ImageTag> <hostIP/ORdns>:5000/<localImage>:<ImageTag>
    docker push <hostIP/ORdns>:5000/<localImage>:<ImageTag> 
    docker image rm <localImage>:<ImageTag>
    docker image rm <hostIP/ORdns>:5000/<localImage>:<ImageTag>
    docker images 

    ## EXAMPLE
     -- My working env -- 
     docker login 192.168.171.97:5000
     docker images 
     docker tag haproxy:latest 192.168.171.97:5000/haproxy:latest
     docker push 192.168.171.97:5000/haproxy:latest 
     docker image rm haproxy:latest 
     docker images | grep haproxy
     docker image rm 192.168.171.97:5000/haproxy:latest 
     
     -- Oficial doc example ---
     docker pull hello-world
     docker tag hello-world localhost/hello-world:latest
     docker tag hyper/docker-registry-web:auth-experimental localhost/docker-registry-web:latest
     docker push localhost/hello-world:latest
     docker push localhost/docker-registry-web:latest

#### and then pull

    docker rmi localhost/hello-world:latest
	docker run localhost/hello-world:latest
	
#### Check web registry for changes
![Repo](https://github.com/konrad2415/docker-registry-UI/blob/master/images/repo.gif)
