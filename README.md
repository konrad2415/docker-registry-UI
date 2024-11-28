## Example configuration for [docker-registry-web](https://github.com/mkuchin/docker-registry-web)

#### Before start: install docker
  

#### How to run:
    
    curl -L https://github.com/konrad2415/docker-registry-UI/archive/refs/heads/master.zip | tar -xzv
    cd examples/nginx-auth-enabled/
    ./generate-keys.sh
    docker-compose up
    

#### Create test user:
![Creating user](https://github.com/konrad2415/docker-registry-UI/blob/master/images/create-test.gif)
                 

#### Push some images

    docker login localhost
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
