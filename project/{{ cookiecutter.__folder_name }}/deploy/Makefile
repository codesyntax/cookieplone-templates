### Defensive settings for make:
#     https://tech.davis-hansson.com/p/make/
SHELL:=bash
.ONESHELL:
.SHELLFLAGS:=-xeu -o pipefail -O inherit_errexit -c
.SILENT:
.DELETE_ON_ERROR:
MAKEFLAGS+=--warn-undefined-variables
MAKEFLAGS+=--no-builtin-rules

# We like colors
# From: https://coderwall.com/p/izxssa/colored-makefile-for-golang-projects
RED=`tput setaf 1`
GREEN=`tput setaf 2`
RESET=`tput sgr0`
YELLOW=`tput setaf 3`

# Add the following 'help' target to your Makefile
# And add help text after each target name starting with '\#\#'
.PHONY: help
help: ## This help message
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'


.PHONE: stop
stop: ## Stop all services
	@echo "$(RED) ===> Stopping"
	docker compose down

.PHONE: start
start: ## Start all services
	docker compose up -d

.PHONE: start-fg
start-fg: ## Start in foreground
	docker compose up

.PHONE: restart
restart: ## Restart all services
	docker compose down
	docker compose up -d

.PHONE: restart-nginx
restart-nginx: ## Restart nginx
	docker compose down nginx
	docker compose up nginx -d

.PHONE: logs-nginx
logs-nginx: ## Show nginx logs
	docker compose logs -f nginx

.PHONE: logs-backend
logs-backend: ## Show backend logs
	docker compose logs -f backend

.PHONE: upgrade
upgrade: ## Download the new images and restart the services
	docker compose pull
	docker compose down backend
	docker compose up backend -d

.PHONE: full-upgrade
full-upgrade: ## Download the new images and restart the services
	docker compose pull
	docker compose down
	docker compose up -d
