CONTEXT = docker.io/ansibleplaybookbundle
VERSION = latest
IMAGE_NAME = photo-album-demo-api

all: build
build:
	docker build --pull -t ${CONTEXT}/${IMAGE_NAME}:${VERSION} -t ${CONTEXT}/${IMAGE_NAME} .
	@if docker images ${CONTEXT}/${IMAGE_NAME}:${VERSION}; then touch build; fi

push:
	docker push ${CONTEXT}/${IMAGE_NAME}:${VERSION}

test:
	$(eval CONTAINERID=$(shell docker run -tdi -u $(shell shuf -i 1000010000-1000020000 -n 1) ${CONTEXT}/${IMAGE_NAME}:${VERSION}))
	@sleep 2
	@docker exec ${CONTAINERID} ps aux
	@docker exec ${CONTAINERID} curl localhost:8080
	@docker rm -f ${CONTAINERID}

run:
	docker run -tdi -u `shuf -i 1000010000-1000020000 -n 1` -p 8080:8080 ${CONTEXT}/${IMAGE_NAME}:${VERSION}

clean:
	rm -f build
