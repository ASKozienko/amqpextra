APP?=amqpextra
COMPOSE_PROJECT_NAME?=$(APP)-e2e-test
TEST?=./test/e2e/test/...

.PHONY: run
run: clean
	go mod tidy
	go mod vendor
	COMPOSE_PROJECT_NAME=$(COMPOSE_PROJECT_NAME) docker-compose --file docker-compose.yml run $(APP)-e2e-test

.PHONY: clean
clean:
	COMPOSE_PROJECT_NAME=$(COMPOSE_PROJECT_NAME) docker-compose --file docker-compose.yml down --remove-orphans
	COMPOSE_PROJECT_NAME=$(COMPOSE_PROJECT_NAME) docker-compose --file docker-compose.yml down --volumes

.PHONY: enter
enter: clean
	COMPOSE_PROJECT_NAME=$(COMPOSE_PROJECT_NAME) docker-compose --file docker-compose.yml run --entrypoint=bash $(APP)-e2e-test

.PHONY: test
test:
	cd ../../; go test -mod=vendor -race -count=1  -v $(TEST)