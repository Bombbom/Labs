# README
## References 
Repo for [Getting Started with Docker (...and AI)](https://www.amazon.com/dp/1916585302) book.

Folders:

- **ai:** AI chatbot app used in Chapter 7
- **compose-app:** Simple Compose app used in Chapter 6 
- **images:** App used in Chapter 5 
- **node-app:** App used in Chapter 4 
- **wasm:** Deprecated (Wasm content mvoed to Docker Deep Dive book and replaced here with AI chapter)

Docker Hub repo is [here](https://hub.docker.com/repository/docker/nigelpoulton/gsd-book/general).

## Practices 

- Requirements: 
    - WSL 
    - Docker Desktop
    - Intergrate Docker to WSL
    - Git
    - NodeJs - npm - nvm
    - Rust, Enable WebAssembly Extension in Docker Desktop

### 1. Check 
- Check `docker` and `docker compose`  version
```bash
$ docker --version
Docker version 28.4.0, build d8eb465

$ docker compose version
Docker Compose version v2.39.2-desktop.1
```

- Install Multipass

### 2. Running your first containers


```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker images
REPOSITORY                                  TAG                                                                           IMAGE ID       CREATED         SIZE
compose-app-web                             latest                                                                        03f64752cf4f   2 days ago      209MB
node-app                                    latest                                                                        3f9dff8f6ad9   2 days ago      210MB
redis                                       alpine                                                                        987c376c7276   5 weeks ago     100MB
envoyproxy/envoy                            v1.32.6                                                                       16a413173825   4 months ago    224MB
docker/desktop-kubernetes                   kubernetes-v1.32.2-cni-v1.6.0-critools-v1.31.1-cri-dockerd-v0.3.16-1-debian   fdd1722efdcc   7 months ago    596MB
registry.k8s.io/kube-apiserver              v1.32.2                                                                       c47449f3e751   7 months ago    129MB
registry.k8s.io/kube-scheduler              v1.32.2                                                                       45710d74cfd5   7 months ago    93.5MB
registry.k8s.io/kube-controller-manager     v1.32.2                                                                       399aa50f4d13   7 months ago    119MB
registry.k8s.io/kube-proxy                  v1.32.2                                                                       83c025f0faa6   7 months ago    129MB
nigelpoulton/gsd-book                       latest                                                                        1d5294e336af   8 months ago    256MB
kindest/node                                v1.31.1                                                                       cd224d8da58d   11 months ago   1.49GB
registry.k8s.io/etcd                        3.5.16-0                                                                      c6a9d11cc5c0   12 months ago   211MB
docker/desktop-cloud-provider-kind          v0.3.0-desktop.3                                                              c321a5c92549   12 months ago   582MB
docker/desktop-containerd-registry-mirror   v0.0.2                                                                        aadc48ce8960   13 months ago   46.4MB
registry.k8s.io/coredns/coredns             v1.11.3                                                                       9caabbf6238b   14 months ago   85.1MB
registry.k8s.io/pause                       3.10                                                                          ee6521f290b2   16 months ago   1.06MB
docker/desktop-vpnkit-controller            dc331cb22850be0cdd97c84a9cfecaf44a1afb6e                                      7ecf567ea070   2 years ago     47MB
docker/desktop-storage-provisioner          v2.0                                                                          115d77efe6e2   4 years ago     59.2MB
```


```bash
$ docker run -d --name test -p 5555:8080 nigelpoulton/gsd-book
7e47299cb4122febadeaa1da5e8441e715ba23cef8c7663e8492ec3fdaaf21dc

$ docker images
REPOSITORY                                  TAG                                                                           IMAGE ID       CREATED         SIZE
compose-app-web                             latest                                                                        03f64752cf4f   2 days ago      209MB
node-app                                    latest                                                                        3f9dff8f6ad9   2 days ago      210MB
redis                                       alpine                                                                        987c376c7276   5 weeks ago     100MB
envoyproxy/envoy                            v1.32.6                                                                       16a413173825   4 months ago    224MB
docker/desktop-kubernetes                   kubernetes-v1.32.2-cni-v1.6.0-critools-v1.31.1-cri-dockerd-v0.3.16-1-debian   fdd1722efdcc   7 months ago    596MB
registry.k8s.io/kube-apiserver              v1.32.2                                                                       c47449f3e751   7 months ago    129MB
registry.k8s.io/kube-proxy                  v1.32.2                                                                       83c025f0faa6   7 months ago    129MB
registry.k8s.io/kube-scheduler              v1.32.2                                                                       45710d74cfd5   7 months ago    93.5MB
registry.k8s.io/kube-controller-manager     v1.32.2                                                                       399aa50f4d13   7 months ago    119MB
nigelpoulton/gsd-book                       latest                                                                        1d5294e336af   8 months ago    256MB
kindest/node                                v1.31.1                                                                       cd224d8da58d   11 months ago   1.49GB
registry.k8s.io/etcd                        3.5.16-0                                                                      c6a9d11cc5c0   12 months ago   211MB
docker/desktop-cloud-provider-kind          v0.3.0-desktop.3                                                              c321a5c92549   12 months ago   582MB
docker/desktop-containerd-registry-mirror   v0.0.2                                                                        aadc48ce8960   13 months ago   46.4MB
registry.k8s.io/coredns/coredns             v1.11.3                                                                       9caabbf6238b   14 months ago   85.1MB
registry.k8s.io/pause                       3.10                                                                          ee6521f290b2   16 months ago   1.06MB
docker/desktop-vpnkit-controller            dc331cb22850be0cdd97c84a9cfecaf44a1afb6e                                      7ecf567ea070   2 years ago     47MB
docker/desktop-storage-provisioner          v2.0                                                                          115d77efe6e2   4 years ago     59.2MB

$ docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS         PORTS                                         NAMES
7e47299cb412   nigelpoulton/gsd-book   "docker-entrypoint.s…"   9 seconds ago   Up 9 seconds   0.0.0.0:5555->8080/tcp, [::]:5555->8080/tcp   test

$ docker stop test
test

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker start test
test

$ docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS         PORTS                                         NAMES
7e47299cb412   nigelpoulton/gsd-book   "docker-entrypoint.s…"   4 minutes ago   Up 8 seconds   0.0.0.0:5555->8080/tcp, [::]:5555->8080/tcp   test

```

- Access: `http://localhost:5555/`


```bash
$ docker rm test -f
test
```

- Managing containers and images with Docker Desktop

### 3. Containerizing an application

```bash
$ cd gsd-book/
$ ls -l
$ ls -l
total 32
-rw-r--r-- 1 * * 8245 Sep 27 21:44 README.md
drwxr-xr-x 6 * * 4096 Sep 27 21:24 ai
drwxr-xr-x 4 * * 4096 Sep 27 21:24 compose-app
drwxr-xr-x 3 * * 4096 Sep 27 21:24 images
drwxr-xr-x 3 * * 4096 Sep 27 21:24 node-app
drwxr-xr-x 2 * * 4096 Sep 27 21:24 wasm

$ node-app
$ npm ci

added 103 packages, and audited 104 packages in 2s

18 packages are looking for funding
  run `npm fund` for details

2 high severity vulnerabilities

To address all issues, run:
  npm audit fix

Run `npm audit` for details
$ node app.js

$ docker init

Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

? What application platform does your project use? Node
? What version of Node do you want to use? 20.19.5
? Which package manager do you want to use? npm
? What command do you want to use to start the app? node app.js
X Sorry, your reply was invalid: Value is required
? What port does your server listen on? 8080

✔ Created → .dockerignore
✔ Created → Dockerfile
✔ Created → compose.yaml
✔ Created → README.Docker.md

→ Your Docker files are ready!
  Review your Docker files and tailor them to your application.
  Consult README.Docker.md for information about using the generated files.

What's next?
  Start your application by running → docker compose up --build
  Your application will be available at http://localhost:8080

$ ls -la
total 92
drwxr-xr-x   4 * *  4096 Sep 27 21:47 .
drwxr-xr-x   7 * *  4096 Sep 27 21:24 ..
-rw-r--r--   1 * *   621 Sep 27 21:47 .dockerignore
-rw-r--r--   1 * *  1169 Sep 27 21:47 Dockerfile
-rw-r--r--   1 * *   827 Sep 27 21:47 README.Docker.md
-rw-r--r--   1 * *   310 Sep 27 21:24 app.js
-rw-r--r--   1 * *  1686 Sep 27 21:47 compose.yaml
drwxr-xr-x 101 * *  4096 Sep 27 21:45 node_modules
-rw-r--r--   1 * * 42816 Sep 27 21:24 package-lock.json
-rw-r--r--   1 * *   410 Sep 27 21:24 package.json
-rw-r--r--   1 * *  1168 Sep 27 21:24 sample-Dockerfile
-rw-r--r--   1 * *  1685 Sep 27 21:24 sample-compose.yaml
drwxr-xr-x   2 * *  4096 Sep 27 21:24 views
```


```bash
$ cat Dockerfile
# syntax=docker/dockerfile:1

# Comments are provided throughout this file to help you get started.
# If you need more help, visit the Dockerfile reference guide at
# https://docs.docker.com/go/dockerfile-reference/

# Want to help us make this template better? Share your feedback here: https://forms.gle/ybq9Krt8jtBL3iCk7

ARG NODE_VERSION=20.19.5

FROM node:${NODE_VERSION}-alpine

# Use production node environment by default.
ENV NODE_ENV production


WORKDIR /usr/src/app

# Download dependencies as a separate step to take advantage of Docker's caching.
# Leverage a cache mount to /root/.npm to speed up subsequent builds.
# Leverage a bind mounts to package.json and package-lock.json to avoid having to copy them into
# into this layer.
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.npm \
    npm ci --omit=dev

# Run the application as a non-root user.
USER node

# Copy the rest of the source files into the image.
COPY . .

# Expose the port that the application listens on.
EXPOSE 8080

# Run the application.
CMD node app.js
```


```bash
$ docker build -t node-app .
[+] Building 19.8s (13/13) FINISHED                                                                             docker:default
 => [internal] load build definition from Dockerfile                                                                      0.0s
 => => transferring dockerfile: 1.21kB                                                                                    0.0s
 => resolve image config for docker-image://docker.io/docker/dockerfile:1                                                 2.0s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                                                          0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:dabfc0969b935b2080555ace70ee69a5261af8a8f1b4df97b9e7fbcf6  0.0s
 => => resolve docker.io/docker/dockerfile:1@sha256:dabfc0969b935b2080555ace70ee69a5261af8a8f1b4df97b9e7fbcf6722eddf      0.0s
 => [internal] load metadata for docker.io/library/node:20.19.5-alpine                                                    2.6s
 => [auth] library/node:pull token for registry-1.docker.io                                                               0.0s
 => [internal] load .dockerignore                                                                                         0.0s
 => => transferring context: 663B                                                                                         0.0s
 => [stage-0 1/4] FROM docker.io/library/node:20.19.5-alpine@sha256:eabac870db94f7342d6c33560d6613f188bbcf4bbe1f4eb47d5  10.8s
 => => resolve docker.io/library/node:20.19.5-alpine@sha256:eabac870db94f7342d6c33560d6613f188bbcf4bbe1f4eb47d5e2a08e1a3  0.0s
 => => sha256:0de821d16564893ff12fae9499550711d92157ed1e6705a8c7f7e63eac0a2bb9 449B / 449B                                0.6s
 => => sha256:fd345d7e43c58474c833bee593321ab1097dd720bebd8032e75fbf5b81b1e554 1.26MB / 1.26MB                            1.1s
 => => sha256:c88300f8759af46375ccc157a0a0dbf7cdaeded52394b5ce2ce074e3b773fe82 42.75MB / 42.75MB                          8.5s
 => => extracting sha256:c88300f8759af46375ccc157a0a0dbf7cdaeded52394b5ce2ce074e3b773fe82                                 2.0s
 => => extracting sha256:fd345d7e43c58474c833bee593321ab1097dd720bebd8032e75fbf5b81b1e554                                 0.1s
 => => extracting sha256:0de821d16564893ff12fae9499550711d92157ed1e6705a8c7f7e63eac0a2bb9                                 0.0s
 => [internal] load build context                                                                                         0.0s
 => => transferring context: 47.93kB                                                                                      0.0s
 => [stage-0 2/4] WORKDIR /usr/src/app                                                                                    0.2s
 => [stage-0 3/4] RUN --mount=type=bind,source=package.json,target=package.json     --mount=type=bind,source=package-loc  2.4s
 => [stage-0 4/4] COPY . .                                                                                                0.1s
 => exporting to image                                                                                                    1.2s
 => => exporting layers                                                                                                   0.6s
 => => exporting manifest sha256:b3a55e9badb4a0e00f40b765d92434891cd2fa165d9a5044447576eae9c68167                         0.0s
 => => exporting config sha256:c6fdbc4365e6d71716053fcdf83f85697fa6d9bdf12104a783ed1f5c350facdb                           0.0s
 => => exporting attestation manifest sha256:458488e39815ce344938b71633e6ba17830d70de73bcb753afb728eed4fff6e1             0.0s
 => => exporting manifest list sha256:b3bcea21516ff6658b1fb5c9f752225410071677aea88f4724ebe3845e78f8c6                    0.0s
 => => naming to docker.io/library/node-app:latest                                                                        0.0s
 => => unpacking to docker.io/library/node-app:latest                                                                     0.5s

 2 warnings found (use docker --debug to expand):
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 14)
 - JSONArgsRecommended: JSON arguments recommended for CMD to prevent unintended behavior related to OS signals (line 38)

$ docker images
REPOSITORY                                  TAG                                                                           IMAGE ID       CREATED          SIZE
node-app                                    latest                                                                        b3bcea21516f   10 seconds ago   206MB

$ docker run -d --name web -p 8080:8080 node-app
af51bece8de56161355bd275e7eeb278b40b28637ecdae5a4073aedf9537af3a

```
- Acces: http://localhost:8080

```bash
$ docker rm web -f
web

$ docker rmi node-app
Untagged: node-app:latest
Deleted: sha256:b3bcea21516ff6658b1fb5c9f752225410071677aea88f4724ebe3845e78f8c6


```

### 4. Images and Registries

### 5. Multi-container apps with Compose

```bash 
$ ls
Dockerfile  app.py  compose.yaml  requirements.txt  static  templates

$ docker compose up --detach
[+] Running 2/2
 ✔ Container compose-app-store-1  Started                                                                          0.3s
 ✔ Container compose-app-web-1    Started             

$ docker compose ps
NAME                  IMAGE             COMMAND                  SERVICE   CREATED      STATUS          PORTS
compose-app-store-1   redis:alpine      "docker-entrypoint.s…"   store     2 days ago   Up 11 seconds   6379/tcp
compose-app-web-1     compose-app-web   "python app.py"          web       2 days ago   Up 11 seconds   0.0.0.0:5555->8080/tcp, [::]:5555->8080/tcp

$ docker compose ls
NAME                STATUS              CONFIG FILES
compose-app         running(2)          /home/ubuntu2204/getting-started-with-docker/gsd-book/compose-app/compose.yaml

$ docker compose stop
[+] Stopping 2/2
 ✔ Container compose-app-web-1    Stopped                                                                          0.5s
 ✔ Container compose-app-store-1  Stopped                            

$ docker compose restart
[+] Restarting 2/2
 ✔ Container compose-app-store-1  Started                                                                          0.3s
 ✔ Container compose-app-web-1    Started                              

$ docker compose up --pull always --detach
[+] Running 1/1
 ✔ store Pulled                                                                                                    2.1s
[+] Running 2/2
 ✔ Container compose-app-store-1  Running                                                                          0.0s
 ✔ Container compose-app-web-1    Running                                                                          0.0s
ubuntu2204@DESKTOP-B18LD9N:~/Documentation/Labs/gsd-book/compose-app$ docker compose down --rmi all
[+] Running 5/5
 ✔ Container compose-app-store-1  Removed                                                                          0.3s
 ✔ Container compose-app-web-1    Removed                                                                          0.4s
 ✔ Image redis:alpine             Removed                                                                          0.1s
 ✔ Image compose-app-web:latest   Removed                                                                          0.1s
 ✔ Network compose-app_internal   Removed                                                                          0.4s
```

### 6. Docker and WebAssembly

- Rust: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  - Uninstall: `rustup self uninstall`   
- spin:  `https://spinframework.dev/v3/install`
  - Install: `curl -fsSL https://spinframework.dev/downloads/install.sh | bash`
- `rustup target add wasm32-wasip1`
- `spin --version`  
- `spin new hello-world -t http-rust`
- ...


