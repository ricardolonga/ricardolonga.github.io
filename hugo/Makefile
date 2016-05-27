.DEFAULT_GOAL := help

guard-%:
	@ if [ "${${*}}" = ""  ]; then \
		echo "Variable '$*' not set"; \
		exit 1; \
	fi

.PHONY: all
all: build push ## build -> push

.PHONY: build
build: ## Generate static blog files
	hugo -d ../

.PHONY: push
push: guard-MSG ## Commit and push changes to GitHub
	git commit -a -m "$(MSG)"
	git push

.PHONY: server
server: ## Run hugo server
	hugo server -w true

.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'