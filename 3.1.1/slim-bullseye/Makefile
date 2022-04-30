BASE := ghcr.io/fillin-inc/rails
TAG := 3.1.1-slim-bullseye
REPO := ${BASE}:${TAG}

repo:
	@echo ${REPO}

build:
	docker build -t ${REPO} .

size:
	docker images | grep ${BASE} | grep ${TAG} | awk '{print $$NF}'

push:
	docker push ${REPO}

local:
	docker run --rm -it ${REPO} bash
