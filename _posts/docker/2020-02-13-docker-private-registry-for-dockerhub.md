---
date: 2020-02-13 18:00:00
layout: post
title: DockerHub를 이용하여 image를 pull/push 해보자!
subtitle: Docker image pull/push for DockerHub 
description: 누구나 쉽게 따라 할 수 있는 DockerHub를 통한 이미지 업/다운로드
image: /assets/img/banner/docker.png
optimized_image: /assets/img/banner/docker.png
category: docker
tags:
  - Docker
  - DockerHub
author: madfalc0n
paginate: true
comments: true
toc: true
---

기본적으로 개인 repository 를 구성하기 위해서는 2가지의 방법이 있다. 첫 번째는 오늘 얘기할 Dockerhub 사이트를 이용하는 방법이고 두 번째는 개인 도커환경에서 repository를 구성하는 방법이다. 개인 도커환경에서 repository를 구축 할 경우 과정이 조금 복잡할 수 있어 첫 번째 방법에 대해서만 진행하겠다.

## 1. [Dockerhub](https://hub.docker.com) 회원가입

`Dockerhub`에 회원가입을 진행한다.

<img src="/assets/img/contents/docker/docker-private-registry-for-dockerhub/image-20200220171558331.png" alt="image-20200220171558331" style="zoom:80%;" />

## 2. Shell에서 `docker login` 입력 후 회원가입한 ID와 비밀번호 입력
```bash
- EX) ID가 chadool116일 경우
	madfalcon@test_madfalcon_server:~$ docker login 
		Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
		
		Username: chadool116 <- dockerhub에서 가입한 아이디
		Password:            <- 비밀번호, 입력해도 화면에 보이지 않는다.
		
		WARNING! Your password will be stored unencrypted in /home/madfalcon/.docker/config.json.
		Configure a credential helper to remove this warning. See
		https://docs.docker.com/engine/reference/commandline/login/#credentials-store

		Login Succeeded
	madfalcon@test_madfalcon_server:~$
```

## 3. `tag` 명령어를 이용하여 생성한 이미지를 다음과 같이 복사
 - 'madfalcon/node-web-app'를 다음의 명령어로 태깅할 수 있음
 - "docker tag [기존이미지] [회원가입ID/생성한이미지파일]"
 - 예시) "docker tag madfalcon/node-web-app:latest chadool116/node-web-app"
```bash
	madfalcon@test_madfalcon_server:~$ docker images
		REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
		madfalcon/node-web-app   latest              77f343714c04        8 days ago          109MB
		node                     alpine3.10          fac3d6a8e034        9 days ago          106MB
		hello-world              latest              fce289e99eb9        11 months ago       1.84kB
		
	madfalcon@test_madfalcon_server:~$ docker tag madfalcon/node-web-app:latest chadool116/node-web-app

	madfalcon@test_madfalcon_server:~$ docker images
		REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
		madfalcon/node-web-app    latest              77f343714c04        8 days ago          109MB
		chadool116/node-web-app   latest              77f343714c04        8 days ago          109MB
		node                      alpine3.10          fac3d6a8e034        9 days ago          106MB
		hello-world               latest              fce289e99eb9        11 months ago       1.84kB
```

## 4. `push` 명령어를 이용해 Dockerhub의 private registry에 업로드
 - "docker push [회원가입ID/생성한이미지파일]"
 - 예시) "docker push chadool116/node-web-app"
 - push 후 dockerhub에서 이미지가 업로드 되었음을 확인할 수 있음
```bash
	madfalcon@test_madfalcon_server:~$ docker push chadool116/node-web-app
		The push refers to repository [docker.io/chadool116/node-web-app]
		83a088502ffd: Pushed 
		4c66dc201393: Pushed 
		f845fd53498a: Pushed 
		f7eb0a63edef: Pushed 
		20d6ac69de87: Mounted from library/node 
		15b7d94033f5: Mounted from library/node 
		4322be3f308a: Mounted from library/node 
		77cae8ab23bf: Mounted from library/node 
		latest: digest: sha256:c591c96e1864d2685a6690daa8e053012c3958197ac70cc4abdbd1637447aa18 size: 1990
	madfalcon@test_madfalcon_server:~$
```

<img src="/assets/img/contents/docker/docker-private-registry-for-dockerhub/image-20200220171911238.png" alt="image-20200220171911238" style="zoom:80%;" />

push가 제대로 이루어졌다면 `dockerhub`에서 업로드 된 이미지 정보를 확인할 수 있다.

## 5. pull 명령어를 이용해 Dockerhub에 업로드한 이미지 가져오기

 - "docker pull [업로드한 이미지]
 - 예시) "docker pull chadool116/node-web-app"
```bash
	madfalcon@test_madfalcon_server:~$ docker images
		REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
		madfalcon/node-web-app   latest              77f343714c04        8 days ago          109MB
		node                     alpine3.10          fac3d6a8e034        9 days ago          106MB
		hello-world              latest              fce289e99eb9        11 months ago       1.84kB

	madfalcon@test_madfalcon_server:~$ docker pull chadool116/node-web-app
		Using default tag: latest
		latest: Pulling from chadool116/node-web-app
		Digest: sha256:c591c96e1864d2685a6690daa8e053012c3958197ac70cc4abdbd1637447aa18
		Status: Downloaded newer image for chadool116/node-web-app:latest
		docker.io/chadool116/node-web-app:latest

	madfalcon@test_madfalcon_server:~$ docker images
		REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
		chadool116/node-web-app   latest              77f343714c04        8 days ago          109MB
		madfalcon/node-web-app    latest              77f343714c04        8 days ago          109MB
		node                      alpine3.10          fac3d6a8e034        9 days ago          106MB
		hello-world               latest              fce289e99eb9        11 months ago       1.84kB
```
