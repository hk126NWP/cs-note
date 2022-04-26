# cs-note

## Table of Contents
[Anaconda](https://github.com/hk126NWP/cs-note/edit/main/README.md#anaconda)\
[Docker](https://github.com/hk126NWP/cs-note/edit/main/README.md#docker)
1. [Docker-WRF](https://github.com/hk126NWP/cs-note/edit/main/README.md#docker-wrf)

# Anaconda
```
> conda --version
> conda update conda
> conda --help
> conda info -e

> conda create --name xxx python=3.8
> conda activate xxx
> conda deactivate
> conda list
> conda install -n xxx [package]
> conda remove xxx
```
# Docker
Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.\
Docker 是屬於另外一種虛擬化技術，它透過 container 的方式將應用程式與相關所需的執行環境包起來，讓每個應用程式共用系統核心（kernel），但還是都有各自獨立的根目錄、檔案系統、網路環境、行程管理等，對於程式而言就好像在一般的獨立的系統上執行一樣。它有三大核心概念，分別是映像檔（Image）、容器（Container）及倉庫（Repository），我們透過將唯讀的映像檔，再用該映像檔創立一個容器，容器可以說是一個輕量的沙箱，每個都是彼此獨立運作，互不影響，也能說容器是映像檔所創造的執行實例，最後我們還能透過倉庫來集中存放及管理映像檔，這可以在本機上做，也能在雲端上做.\
```
> sudo apt-get remove docker docker-engine docker.io # remove any older version 
> sudo apt-get install docker.io
> service docker status
> sudo usermod -aG docker username # add user into docker group
> docker version
> docker -v
```
## Obtain the Docker container image
### Search, Pull, list all images and list activated containers
```
> docker search xxx
> docker pull xxx
> docker images
> docker ps
> docker stats 來查看目前容器使用資源的狀況
```
### Running programe in container
```
> docker run xxx /bin/echo 'Hello world'
```
### Interactive mode
```
> docker run -it xxx /bin/bash
> exit 
```
### Check info of container
```
docker inspect container-xxx
```
### Volume
Docker 提供另一種容器 Volume 來解決著個問題，我們可以把它視為獨立的可讀寫的容器，更重要的是 Volume 不會隨著容器的移除而跟著移除,當你使用 volume 時，docker 會在你的本機上隨機新增一個資料夾（Local storage area），大部分會在 /var 底下，然後讓這個資料夾跟 container 裡面的某個資料夾互通。因為他們是互通的，所以當你 container 裡面那個資料夾有任何變更時，本地的資料夾也會跟著變，而且很重要的一點是：container 被刪掉時那個資料夾還會原封不動保留在那邊
#### Host Volume
```
> ls /home/user1/storage
> docker run -it -v /home/user1/storage:/storage centos /bin/bash # home-dir:container-dir Image Command
> ls /home/user1/storage
```
## Docker-WRF
