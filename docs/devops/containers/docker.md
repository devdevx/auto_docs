# Docker

## Commands

Add credentials

````
docker login -u <username> -p <deploy_token> registry.example.com
````


````
\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\
````

## Info

Prefer COPY over ADD, use ADD to download files or to extract archives

````
# download external file
ADD https://source.com/file /destination/path

# copy and extract content
ADD source.file.tar.gz /destination/path
````

## Optimize images

TODO

https://jpetazzo.github.io/2020/02/01/quest-minimal-docker-images-part-1/

https://jpetazzo.github.io/2020/03/01/quest-minimal-docker-images-part-2/

https://jpetazzo.github.io/2020/04/01/quest-minimal-docker-images-part-3/

