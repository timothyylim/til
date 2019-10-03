# Docker

### Info
* An instance of an image is called a container


### Commands
* docker ps //show only running containers
* docker ps -a //show all containers
* docker run -it image_name sh //Get inside docker container, use ps to get image name
* docker pull image:tag e.g. helloworld:2.5.2 (2.5.2 is the tag, pulls latest by default)

* #### -it flag:
  It means you can log in to your container using TTY, ie terminal. It's as if you've got a Linux machine in front of you and you're logging into it. If you have a container that's not running SSH server or telnet, this is your only mode of getting into the command line prompt.
* #### --rm flag:
  Docker also removes the anonymous volumes associated with the container when the container is removed. 

### Links
* https://www.fpcomplete.com/blog/2017/12/building-haskell-apps-with-docker
* https://docs.haskellstack.org/en/stable/docker_integration/

  
