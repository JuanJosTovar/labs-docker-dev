# Documentación Primer Laboratorio

# Imagen oficial de Ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
9c704ecd0c69: Pull complete 
Digest: sha256:2e863c44b718727c860746568e1d54afd13b2fa71b160f5cd9058fc436217b30
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

# Versión de python (3.9)
3.9: Pulling from library/python
ca4e5d672725: Pull complete 
30b93c12a9c9: Pull complete 
10d643a5fa82: Pull complete 
d6dc1019d793: Pull complete 
c387064957b7: Pull complete 
26766ebde481: Pull complete 
8a42d17fd0e2: Pull complete 
79eda865cc8a: Pull complete 
Digest: sha256:fea84f3a3b72c41efe7fc3b07ae209c6856b852b942c05fa88b747b74f70e711
Status: Downloaded newer image for python:3.9
docker.io/library/python:3.9

# Ejecutar el contenedor de Ubuntu en modo interactivo
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker run -it ubuntu bash
root@79ea6271f1de:/#

# Pull de images de Apache
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker pull httpd
Using default tag: latest
latest: Pulling from library/httpd
efc2b5ad9eec: Pull complete 
fce1785eb819: Pull complete 
4f4fb700ef54: Pull complete 
f214daa0692f: Pull complete 
05383fd8b2b3: Pull complete 
88ad12232aa1: Pull complete 
Digest: sha256:932ac36fabe1d2103ed3edbe66224ed2afe0041b317bcdb6f5d9be63594f0030
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest

# Ejecuta un servidor web Apache en segundo plano, mapeando el puerto 8000 del host al puerto 80 del contenedor
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker run -d -p 8000:80 httpd
7f4fa62c439e94a6433f1fd0de5cc4c8c60a6116209c1c9929fb450e5f1f56bd


# Visualizar todos los contenedores
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND              CREATED          STATUS                     PORTS                                   NAMES
7f4fa62c439e   httpd     "httpd-foreground"   4 minutes ago    Up 4 minutes               0.0.0.0:8000->80/tcp, :::8000->80/tcp   beautiful_babbage
79ea6271f1de   ubuntu    "bash"               12 minutes ago   Exited (0) 6 minutes ago                                           thirsty_hugle


# Eliminar contenedor Ubuntu
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker rm 79ea6271f1de
79ea6271f1de

# Visualizar que se haya eliminado
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND              CREATED         STATUS         PORTS                                   NAMES
7f4fa62c439e   httpd     "httpd-foreground"   6 minutes ago   Up 6 minutes   0.0.0.0:8000->80/tcp, :::8000->80/tcp   beautiful_babbage

# Eliminar todos los contenedores detenidos
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker container prune -f
Total reclaimed space: 0B

# Comando para contruir imagen con ubuntu
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker build -t ubuntu-updated:latest .
[+] Building 9.5s (6/6) FINISHED                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                  0.2s
 => => transferring dockerfile: 96B                                                                                   0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                      0.0s
 => [internal] load .dockerignore                                                                                     0.2s
 => => transferring context: 2B                                                                                       0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                        0.1s
 => [2/2] RUN apt-get update && apt-get upgrade -y                                                                    7.8s
 => exporting to image                                                                                                0.7s
 => => exporting layers                                                                                               0.5s
 => => writing image sha256:66d1e4f0dc0b92485369fc7caeaefe890abb619a700c2c98f17d9ad11497ce4a                          0.0s
 => => naming to docker.io/library/ubuntu-updated:latest

# Instalar Nginx en Ubuntu
 @JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker build -t ubuntu-updated:latest .
[+] Building 13.6s (6/6) FINISHED                                                                           docker:default
 => [internal] load build definition from Dockerfile                                                                  0.1s
 => => transferring dockerfile: 138B                                                                                  0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                      0.0s
 => [internal] load .dockerignore                                                                                     0.1s
 => => transferring context: 2B                                                                                       0.0s
 => CACHED [1/2] FROM docker.io/library/ubuntu:latest                                                                 0.0s
 => [2/2] RUN apt-get update && apt-get install -y nginx                                                             12.2s
 => exporting to image                                                                                                1.0s
 => => exporting layers                                                                                               0.9s
 => => writing image sha256:a83fbc34f1b55499c5575eada69e4a692db0f5f1192b9f469b4bcd9d313de0a6                          0.0s
 => => naming to docker.io/library/ubuntu-updated:latest

# Construir imagen de Nginx
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker build -t my-nginx:latest .
[+] Building 0.5s (6/6) FINISHED                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                  0.1s
 => => transferring dockerfile: 138B                                                                                  0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                      0.0s
 => [internal] load .dockerignore                                                                                     0.1s
 => => transferring context: 2B                                                                                       0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                        0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                       0.0s
 => exporting to image                                                                                                0.1s
 => => exporting layers                                                                                               0.0s
 => => writing image sha256:a83fbc34f1b55499c5575eada69e4a692db0f5f1192b9f469b4bcd9d313de0a6                          0.0s
 => => naming to docker.io/library/my-nginx:latest 

 # Ejecutar imagen de Nginx
 @JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker run -d -p 80:80 my-nginx:latest
397d88a49318f74287d3732d6f395063181cd8b67920fb3b243559bcb9681589

# Modificar el Dockerfile de Nginx para exponer el puerto 80
# Reconstruir
@JuanJosTovar ➜ /workspaces/labs-docker-dev (main) $ docker build -t my-nginx:latest .
[+] Building 0.6s (6/6) FINISHED                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                  0.1s
 => => transferring dockerfile: 147B                                                                                  0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                      0.0s
 => [internal] load .dockerignore                                                                                     0.0s
 => => transferring context: 2B                                                                                       0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                        0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                       0.0s
 => exporting to image                                                                                                0.1s
 => => exporting layers                                                                                               0.0s
 => => writing image sha256:c62dc78350be8f72f188405594459be6a9fd50aad1d50929b70bc1b2070590e7                          0.0s
 => => naming to docker.io/library/my-nginx:latest   