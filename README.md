# debian-docker-vagrant
~~~~
> del Vagrantfile
>vagrant init --template Vagrantfile.provision.bash.erb
>dir
>vagrant up "vg-debian-04"


>vagrant destroy -f "vg-debian-04"

>vagrant global-status

>del Vagrantfile
>dir
~~~~
~~~~

vagrant up vg-debian-03
cd /vagrant/dockerfiles/multi/

#docker build --no-cache  
#force rebuilding of layers already available,force the execution of each step/instruction in the Dockerfile

sudo docker build -t devopscube/node-app:1.0-nocache --no-cache -f Dockerfile.single .

sudo docker build -t devopscube/node-app:1.0-cache -f Dockerfile.single .

$ sudo docker image ls
REPOSITORY            TAG           IMAGE ID       CREATED         SIZE
devopscube/node-app          1.0-cache                  8dc5fd7228bd   About a minute ago   910MB
devopscube/node-app          1.0-nocache                8dc5fd7228bd   About a minute ago   910MB
~~~~

~~~~
vagrant up vg-debian-03
cd /vagrant/dockerfiles/multi/

sudo docker build -t devopscube/node-app-multi:1.0-alpine --no-cache -f Dockerfile.multi.alpine  .
sudo docker build -t devopscube/node-app-multi:1.0-distroless --no-cache -f Dockerfile.multi.distroless  .
sudo docker build -t devopscube/node-app-single:1.0 --no-cache -f Dockerfile.single .
sudo docker build -t devopscube/node-app-multi:1.0-debian-bullseye-slim --no-cache -f Dockerfile.multi.debian  .

$ sudo docker image ls
REPOSITORY                   TAG              IMAGE ID       CREATED          SIZE
devopscube/node-app-single   1.0              e8b38386a0dc   2 minutes ago    910MB
devopscube/node-app-multi    1.0-debian-bullseye-slim   e4a8a36e1480   21 seconds ago       245MB
devopscube/node-app-multi    1.0-alpine       ad41c10f6698   4 minutes ago    171MB
devopscube/node-app-multi    1.0-distroless   e1b409353121   3 minutes ago    118MB


~~~~
~~~~
$ sudo docker history --human --format "{{.ID}} {{.CreatedBy}}: {{.Size}}" devopscube/node-app-single:1.0
e8b38386a0dc /bin/sh -c #(nop)  CMD ["node" "index.js"]: 0B
11c8ef8378db /bin/sh -c #(nop)  EXPOSE 3000: 0B
d6c533204e75 /bin/sh -c npm install: 5.03MB
8b7a6b2be79d /bin/sh -c #(nop) COPY dir:9301d0637515751ac…: 1.4kB
842962c4b3a7 /bin/sh -c #(nop)  CMD ["node"]: 0B
<missing> /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…: 0B
<missing> /bin/sh -c #(nop) COPY file:4d192565a7220e13…: 388B
<missing> /bin/sh -c set -ex   && for key in     6A010…: 7.59MB
<missing> /bin/sh -c #(nop)  ENV YARN_VERSION=1.22.15: 0B
<missing> /bin/sh -c ARCH= && dpkgArch="$(dpkg --print…: 92.9MB
<missing> /bin/sh -c #(nop)  ENV NODE_VERSION=16.13.2: 0B
<missing> /bin/sh -c groupadd --gid 1000 node   && use…: 334kB
<missing> /bin/sh -c set -ex;  apt-get update;  apt-ge…: 510MB
<missing> /bin/sh -c apt-get update && apt-get install…: 146MB
<missing> /bin/sh -c set -ex;  if ! command -v gpg > /…: 17.5MB
<missing> /bin/sh -c set -eux;  apt-get update;  apt-g…: 16.5MB
<missing> /bin/sh -c #(nop)  CMD ["bash"]: 0B
<missing> /bin/sh -c #(nop) ADD file:be998d04a8927e9c4…: 114MB

$ sudo docker history --human --format "{{.ID}} {{.CreatedBy}}: {{.Size}}" devopscube/node-app-multi:1.0-alpine
ad41c10f6698 /bin/sh -c #(nop)  CMD ["index.js"]: 0B
da5b41b925fb /bin/sh -c #(nop)  EXPOSE 8080: 0B
6bad03b453c5 /bin/sh -c #(nop) COPY dir:fda48d9f47f743506…: 1.76MB
025c3cbb849f /bin/sh -c #(nop)  CMD ["node"]: 0B
<missing> /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…: 0B
<missing> /bin/sh -c #(nop) COPY file:4d192565a7220e13…: 388B
<missing> /bin/sh -c apk add --no-cache --virtual .bui…: 7.76MB
<missing> /bin/sh -c #(nop)  ENV YARN_VERSION=1.22.17: 0B
<missing> /bin/sh -c addgroup -g 1000 node     && addu…: 156MB
<missing> /bin/sh -c #(nop)  ENV NODE_VERSION=17.4.0: 0B
<missing> /bin/sh -c #(nop)  CMD ["/bin/sh"]: 0B
<missing> /bin/sh -c #(nop) ADD file:9233f6f2237d79659…: 5.59MB


$ sudo docker history --human --format "{{.ID}} {{.CreatedBy}}: {{.Size}}" devopscube/node-app-multi:1.0-distroless
e1b409353121 /bin/sh -c #(nop)  CMD ["index.js"]: 0B
a3a60bcb1b40 /bin/sh -c #(nop)  EXPOSE 3000: 0B
4b3536de4c9d /bin/sh -c #(nop) COPY dir:fda48d9f47f743506…: 1.76MB
fa463f9d1f7c bazel build ...: 93.3MB
<missing> bazel build ...: 2.34MB
<missing> bazel build ...: 17.9MB
<missing> bazel build ...: 2.36MB

$ sudo docker history --human --format "{{.ID}} {{.CreatedBy}}: {{.Size}}" devopscube/node-app-multi:1.0-debian-bullseye-slim
e4a8a36e1480 /bin/sh -c #(nop)  CMD ["index.js"]: 0B
0cd8d3500cb5 /bin/sh -c #(nop)  EXPOSE 8080: 0B
9e9b9942f574 /bin/sh -c #(nop) COPY dir:fda48d9f47f743506…: 1.76MB
41bfb961e3ef /bin/sh -c #(nop)  CMD ["node"]: 0B
<missing> /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…: 0B
<missing> /bin/sh -c #(nop) COPY file:4d192565a7220e13…: 388B
<missing> /bin/sh -c set -ex   && savedAptMark="$(apt-…: 9.48MB
<missing> /bin/sh -c #(nop)  ENV YARN_VERSION=1.22.17: 0B
<missing> /bin/sh -c ARCH= && dpkgArch="$(dpkg --print…: 153MB
<missing> /bin/sh -c #(nop)  ENV NODE_VERSION=17.4.0: 0B
<missing> /bin/sh -c groupadd --gid 1000 node   && use…: 333kB
<missing> /bin/sh -c #(nop)  CMD ["bash"]: 0B
<missing> /bin/sh -c #(nop) ADD file:09675d11695f65c55…: 80.4MB

~~~~

~~~~
https://github.com/wagoodman/dive

sudo dive devopscube/node-app-single:1.0

Total Image size: 910 MB                                                                                 
Potential wasted space: 10 MB                                                                             
Image efficiency score: 99 %



sudo dive devopscube/node-app-multi:1.0-distroless

Total Image size: 118 MB                                                                                  
Potential wasted space: 0 B                                                                               
Image efficiency score: 100 %

sudo dive devopscube/node-app-multi:1.0-alpine  

Total Image size: 171 MB                                                                                  
Potential wasted space: 704 kB                                                                            
Image efficiency score: 99 %

sudo dive devopscube/node-app-multi:1.0-debian-bullseye-slim

Total Image size: 245 MB                                                                                  
Potential wasted space: 6.0 MB                                                                            
Image efficiency score: 98 %
~~~~
~~~~
https://github.com/docker-slim/docker-slim

curl -L -o ds.tar.gz https://downloads.dockerslim.com/releases/1.37.3/dist_linux.tar.gz
tar -xvf ds.tar.gz
mv dist_linux/docker-slim* /usr/local/bin
docker-slim
~~~~