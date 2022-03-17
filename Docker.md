---
title: Docker
date: 2022-03-16
update: 2022-03-16
---



#### What is Docker ?

-----

Là container để chạy các application trong một môi trường cô lập tài nguyên (isolation)

|                            Docker                            |                             VMs                             |
| :----------------------------------------------------------: | :---------------------------------------------------------: |
|  Process trong container sử dụng trực tiếp tài nguyên thật   |                  Giới hạn bởi phần cứng ảo                  |
|               Hệ điều hành thật chạy phần mềm                |                Hệ điều hành ảo chạy phần mềm                |
| Chia sẻ chung tài nguyên với hệ điều hành thật nên chạy nhanh hơn | Có hệ điều hành riêng với tài nguyên riêng và chạy chậm hơn |



#### Docker Images

---------

Bản sao của container (blueprint) nhưng ko chạy mà chỉ để lưu lại container

* Runtime enviroment
* Application code
* Dependencies
* Extra configuration (env variables)
* Command

Image chứa thông tin của container. 

```mermaid
graph LR
    A[Image] -->| run | B[Container]
```

#### Container

-----------

Được biết đến là tiến trình được cô lập (***Isolated process***): chạy độc lập với các tiến trình đang chạy khác trên máy tính.

Container là một instance của image được khởi chạy



#### Parent Images

-------------

Image được tạo nên từ nhiều lớp ```(layers)``` 

Parent Image là lớp đầu tiên bao gồm hệ điều hành và có thể là mỗi trường khởi chạy ứng dụng ``(runtime enviroment: node, py,...)``

Các layers tiếp theo có thể là bất kỳ thứ gì: source code, dependencies,...



#### Docker Hub

------------

Online repository dành cho docker image ``(Khá tương đồng với Github)``



#### Dockerfile - Docker Command

------------

Tạo ra docker image.

> .dockerignore ignore any file

***

```dockerfile
FROM <parent_image>:<tag - optional ?>

WORKDIR <root_directory>

COPY <from_source_code> <to_directory_in_workdir>

RUN <install dep - making the image so dont run app here>

EXPOSE <export_port>

CMD [<run app in container>]
```

> Từng command là từng layer được add vào image

EX:

```dockerfile
FROM node:17-alpine

WORKDIR /app

COPY . .

RUN npm i

EXPOSE 4000

CMD ["npm","start"]
```

Build

```dockerfile
docker build -t <image_name>:<tag - optional> .
```

> **Layer caching** : docker lưu các layer vào cache nên cùng image được build nhanh hơn sau lần đầu tiên

Run

```dockerfile
docker run --name <container_name> -p <local_port:image_port> <image_name>

docker start <container>
```

> -d : start container in background
>
> -i: start container normal not in background

> start: run container có sẵn
>
> run: tạo mới container

Listing images

```dockerfile
docker images
```

Remove images

```dockerfile
docker image rm <image>
```

> -f : force remove

Execute command inside container

```dockerfile
docker container exec <container>

docker exec -it <container> /bin/sh
```

Stop container

```dockerfile
docker stop <container>
```

Remove container

```dockerfile
docker container rm <container>
```

Listing container

```dockerfile
docker ps -a<<list offline container>>
```



#### Volume

------------

Thay đổi source code => build image mới

Volume là tính năng của docker cho phép chỉ định folder trên máy host và ánh xạ tới folder trong container => thay đổi source không cần build lại image

```dockerfile
docker run ... -v <host_folder>:<map_folder> <container>
```

> -rm : remove container after stop

**node_modules problem:**  mapping node modules từ host tới container là ko cần thiết nhưng cũng ko thể xoá node modules trên host vì khi map node modules trong container cũng bị xoá theo

=> Thêm volume mới chỉ định vị trí folder node modules bên trong container và ko ánh xạ từ folder trên host tới volume đầu nữa mà chỉ ánh xạ tới folder được quản lý bởi docker.

```dockerfile
-v <host_folder>:<map_folder> -v <root_app>/node_modules <container>
```



> Sử dụng volume các node app thì chỉ cần copy package.json trong dockerfile rồi chỉ định volume trong docker-compose chứ ko cần copy cả source code



#### Docker Compose

-----

config run nhiều container cùng lúc, các container dễ dàng giao tiếp với nhau

**Structure**

```dockerfile
version: "<>"
services:
	<service_name>:
		build: <root_app>
		container_name: <name>
		ports:
			- '<host_port>:<app_port>'
		volumes:
			- <relative_path_folder>:<container_folder>
			- <root_app>/node_modules
```

> with react-app: 
>
> ​	stdin_open: true
>
> ​	tty: true	

Build 

> same folder with docker-compose.yaml file

```dockerfile
docker-compose up
```

