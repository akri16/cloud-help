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
- Docker doesn't connect to STDOUT, so you won't see the logs if you run a detached container<br>
`docker logs <container-id>`

- You need to investigate only when the Exit condition is (1). (0) is normal exit

### Container Images
- Basically a tar file with associated metadata
- Build images on top of a base image layer
- Each modification adds a layer. Try to reduce the number of layers as much as possible

Show or remove Images <br>
`docker image ls|rm <img id>`

Show differnet layers in the image <br>
`docker history <image:tag>`

Tag an image <br>
`docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

- You can create an image using:
  1) `docker commit` on a running container after applying the modifications
  2) Using a <i> Dockerfile </i>

### Image creation using a Dockerfile
- You should start by creating a working directory for your project.
- FROM: Specify the Base Image
- MAINTAINER: maintainer
- RUN: Executes a command
  - Don't run multiple RUN commands as it'll create separate layers
  - Use: <br>
      ```
      cmd1 && \
      cmd2 && \
      cmd3 &&
      ```
- EXPOSE: Has metadata options on where the image should run
- ENV: Environment variables (Not a good practice to hardcode)
- ADD/COPY: copy files
- USER: username for the RUN, CMD commands
- CMD: Starting command. Reccommended as it can be overwritten while running the image
- ENTRYPOINT: Starting point that can't be overwritten
  - Provide arguments in CMD and the shell environment in ENTRYPOINT
  - Exec Form (JSOn array of items): ["<w1>", "<w2>", ...] notation to specify commands
  - Shell Form: Normal command option (One single string)

Build an image from the working directory <br>
`docker build -t [--no-cache] <tag>`
  
  


