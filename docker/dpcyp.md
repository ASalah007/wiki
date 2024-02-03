# Docker practical course

- 1-way binding is when you bind a host port/folder to a container port/folder but not the other way around.
  (changes in the host folder will be reflected in the container folder but not vice versa)

  `docker run -d -v /dir/in/host:/dir/in/container:ro -p 8080:80 nodeapp`

- 2-way binding is when you bind a host port/folder to a container port/folder and vice versa
  (changes in the host folder will be reflected in the container folder and vice versa).

  `docker run -d -v /dir/in/host:/dir/in/container -p 8080:80 nodeapp`

- **Anonymous** volumes are volumes that are not bound to a host folder.
  this is a way to exclude a folder inside the container from being affected by changes in host folder.

  `docker run -d -v /dir/in/container -p 8080:80 nodeapp`

## video 14

- `docker inspect <container>`: shows information about container
- there are two different types of volumes:
  1. bind mount `/dir/on/host:/dir/on/container`
  2. `volume-name:/dir/on/container`
