### docs
- http://localhost:8080/
- https://bziwnsizd.tistory.com/54
- https://hub.docker.com/u/seunggab

### start
```shell
brew install node
node app.js
```
```shell
docker build -t kubia .
docker images
REPOSITORY               TAG             IMAGE ID       CREATED         SIZE
kubia                    latest          8d8e6ab95d50   5 minutes ago   660MB

docker run --name kubia-container -p 8080:8080 -d kubia # port, detach(background) <id>
curl localhost:8080

echo $DOCKER_HOST

docker ps
docker inspect kubia-container
```
```shell
docker exec -it kubia-container bash

root@7e9d3c774880:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  1.0  1.3 791000 105472 ?       Ssl  05:38   0:01 /usr/bin/qemu-x86_64 /usr/local/bin/node node app.js
root        14  0.3  0.1 169256 11028 pts/0    Ssl  05:40   0:00 /usr/bin/qemu-x86_64 /bin/bash bash
root        22  0.0  0.1 166136  9536 ?        Rl+  05:04   0:00 ps aux
root@7e9d3c774880:/# ps aux | grep app.js
root         1  0.8  1.3 791000 105472 ?       Ssl  05:38   0:01 /usr/bin/qemu-x86_64 /usr/local/bin/node node app.js
root        27  3.0  0.1 159484  8504 pts/0    Sl+  05:41   0:00 /usr/bin/qemu-x86_64 /bin/grep grep app.js

➜  ~ ps aux | grep app.js
seunggab.kim     69074   0.0  0.0 408628368   1616 s003  S+    2:42PM   0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox app.js
```
```shell
docker stop kubia-container
docker rm kubia-container

docker tag kubia seunggab/kubia
docker push seunggab/kubia
docker run --name kubia-container -p 8080:8080 -d seunggab/kubia
```