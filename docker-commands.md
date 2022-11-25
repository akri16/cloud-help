- If the shell you are running is an entry point shell then you have to detach from the shell before moving away to prevent stopping the container
- Use Ctrl + P, Ctrl + Q to detach from a running container entrypoint terminal

Run a container from an image <br>
`docker run [-it | -d] [--rm] <img>:<tag> [<CMD>]`

Check the running containers<br>
`docker ps [-a]`

Lifecycle commands <br>
`docker stop/kill/restart/rm`

Inspect a container<br>
`docker inspect [--format={{<FORMAT>}}] <container-id>`

### Logging
- Docker doesn't connect to STDOUT, so you won't see the logs if you run a detached container
`docker logs <container-id>`

- You need to investigate only when the Exit condition is (1). (0) is normal exit

### Container Images
- Basically a tar file with associated metadata
- Build images on top of a base image layer
- Each modification adds a layer. Try to reduce the number of layers as much as possible

Show or remove Images
`docker image ls|rm <img id>`

Show differnet layers in the image
`docker history <image:tag>`

Tag an image
`docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

- You can create an image using:
  1) `docker commit` on a running container after applying the modifications
  2) Using a <i> Dockerfile </i>




