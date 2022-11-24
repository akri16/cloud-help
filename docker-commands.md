- If the shell you are running is an entry point shell then you have to detach from the shell before moving away to prevent stopping the container
- Use Ctrl + P, Ctrl + Q to detach from a running container entrypoint terminal

Run a container from an image <br>
`docker run [-it | -d] [--rm] <img>:<tag> [<CMD>]`

Check the running containers
docker ps [-a]

Lifecycle commands <br>
`docker stop/kill/restart/rm`

Inspect a container
`docker inspect [--format={{<FORMAT>}}] <container-id>`
