
# ARCHITECTURE
ARCH ?= amd64
# ARCH = arm64

## REPO INFO
DOCKER_REPO ?= quay.io/toschneck/openvpn-${ARCH}
DOCKER_REPO_MULTI ?= quay.io/toschneck/openvpn
VERSION ?= 0.1.0
FINAL_TAG ?= ${VERSION}
TAG_DATE ?= ${VERSION}-$(shell date -I)

docker-build:
	docker build --pull --build-arg ARCH=${ARCH} -t ${DOCKER_REPO}:${TAG_DATE} .

#docker-run-local: docker-build
	#docker run -it -p 8080:80 ${DOCKER_REPO}:${TAG_DATE}

docker-run-local-bash: docker-build
	docker run -it ${DOCKER_REPO}:${TAG_DATE} bash


# update latest, version ref and set unique tag
docker-release: docker-build
	docker tag ${DOCKER_REPO}:${TAG_DATE} ${DOCKER_REPO}:${FINAL_TAG}
	docker push ${DOCKER_REPO}:${FINAL_TAG}
	docker push ${DOCKER_REPO}:${TAG_DATE}

docker-release-latest: docker-release
	docker tag ${DOCKER_REPO}:${TAG_DATE} ${DOCKER_REPO}:latest
	docker push ${DOCKER_REPO}:latest

# MULTI ARCH
# info: https://medium.com/@life-is-short-so-enjoy-it/docker-how-to-build-and-push-multi-arch-docker-images-to-docker-hub-64dea4931df9
docker-release-multi-arch:
	ARCH=amd64 make docker-release-latest
	ARCH=arm64 make docker-release-latest
	docker manifest create -a ${DOCKER_REPO_MULTI}:${FINAL_TAG} \
		${DOCKER_REPO_MULTI}-amd64:${FINAL_TAG} \
		${DOCKER_REPO_MULTI}-arm64:${FINAL_TAG}
	docker manifest push ${DOCKER_REPO_MULTI}:${FINAL_TAG}

docker-release-multi-arch-latest: docker-release-multi-arch
	docker manifest create -a ${DOCKER_REPO_MULTI}:latest \
    		${DOCKER_REPO_MULTI}-amd64:latest \
    		${DOCKER_REPO_MULTI}-arm64:latest
	docker manifest push ${DOCKER_REPO_MULTI}:latest