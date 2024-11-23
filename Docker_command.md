An example command to create a Docker container is −

```
docker run -i -t ubuntu /bin/bash
```


Useful Docker Image Commands
[+]Listing all Docker Images
```
docker images
docker image ls -q
```

[+]Pulling Docker Images
```
docker pull ubuntu:20.04
```

[+]Building Docker Images from Dockerfile
```
docker build -t myapp:latest .
```

[+]Tagging Docker Images

```
docker tag myapp:latest myrepo/myapp:v1.0
```

[+]Pushing Docker Images
```
docker tag myapp:latest myrepo/myapp:v1.0
```

[+]Removing Docker Images
```
docker rmi myapp:latest
```


[+]Pruning Docker Images
-a, --all − Delete all unused images, not just the dangling ones.
-f, --force − Don't ask for confirmation before cleaning.
 removes unused Docker images from your local machine
```
docker image prune -a
```


[+]Viewing Docker Image History
The docker image history command shows the history of a Docker image, including the commands and instructions used during the image-building process. This can be useful for determining how an image is formed and diagnosing problems.
```
docker image history myimage:latest
```


[+]Inspecting Docker Images
The docker image inspect command returns extensive information about a Docker image in JSON format. This includes the settings, layers, labels, and environment variables. You can use the --format option to format the output with a Go template.
```
docker image inspect myimage:latest
```



[+]How to Delete all Docker Images at Once?
-> Use chain of command
```
docker rmi $(docker image ls -q)
```



