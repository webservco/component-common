# webservco/component-common

Common dependencies for component projects. It holds the shared PHP_CodeSniffer ruleset (`.phpcs/php-coding-standard.xml`, which extends `webservco/coding-standards` with the component namespaces) and the Docker configuration.

---

## Component workflow

### [Create project repository](https://github.com/organizations/webservco/repositories/new)

- public
- leave every other option unchecked (no README, license or `.gitignore`). The repository has to start empty.

### Set up project name

```sh
COMPONENT_NAME='COMPONENT_NAME';
```

### Run customization commands (clone `component-skeleton`)

```sh
cd ~/p/webservco-components && \
git clone git@github.com:webservco/component-skeleton.git $COMPONENT_NAME && \
cd $COMPONENT_NAME && \
git remote set-url origin git@github.com:webservco/$COMPONENT_NAME.git && \
sed -i -e "s|component-skeleton|$COMPONENT_NAME|g" README.md && \
sed -i -e "s|\"name\" : \"webservco/component-skeleton\"|\"name\" : \"webservco/$COMPONENT_NAME\"|g" composer.json && \
sed -i -e "s|name: component-skeleton|name: $COMPONENT_NAME|g" .ddev/config.yaml && \
git add README.md composer.json .ddev/config.yaml && \
git commit -m 'Customize' && \
git push -u origin main
```

The skeleton already contains every directory the checks expect (`bin`, `config`, `docs`, `public`, `resources`, `src/WebServCo`, `tests/Unit/WebServCo`), each kept in git by an empty `.gitkeep`.

### Add code

- Code goes in `src/WebServCo/` (namespace `WebServCo\`), unit tests in `tests/Unit/` (namespace `Tests\Unit\`).
- Delete a directory's `.gitkeep` once it holds real files.
- Fill in the README template. The hidden comment at the top of the file explains how; delete it and the template note when done.
- Set `description` in `composer.json` to the README description ("A PHP component/library." plus one sentence).

### Development

```sh
# Start project.
ddev start
# Install dependencies.
ddev c u
# Run all validations.
ddev c c
# Run unit tests.
ddev c test:dox
```

#### Without ddev (Docker)

Use this only when you can't set up a local environment. Working through Docker this way is more cumbersome.

```sh
# Customize
DOCKER_IMAGE_TAG="webservco-component-${COMPONENT_NAME}";
DOCKER_CONTAINER_NAME="webservco-component-${COMPONENT_NAME}-container";

# Download Docker configuration
curl -sL https://github.com/webservco/component-common/archive/refs/heads/main.tar.gz \
    | tar xz --strip-components=1 component-common-main/.docker

# Build and run
docker build --tag ${DOCKER_IMAGE_TAG} -f .docker/config/php84-cli-copy/Dockerfile .
docker run -it --rm --name ${DOCKER_CONTAINER_NAME} ${DOCKER_IMAGE_TAG} /bin/bash -c "composer check:phpcs"

# Cleanup
docker image rm ${DOCKER_IMAGE_TAG}
```

### Add dependencies

### Publish tag

```sh
git tag vX.Y.Z && git push --tags
```

### [Publish on packagist](https://packagist.org/packages/submit)

### Update index

---

## Index

### Misc

- [webservco/coding-standards (Coding standards, dev dependency)](https://packagist.org/packages/webservco/coding-standards)
- [webservco/component-common (Common dependencies)](https://packagist.org/packages/webservco/component-common)
- webservco/component-skeleton (Project template, not on packagist)
- webservco/http-client-test (test for http-client, not on packagist)

### Components

- [webservco/application](https://packagist.org/packages/webservco/application)
- [webservco/application-default](https://packagist.org/packages/webservco/application-default)
- [webservco/application-runner](https://packagist.org/packages/webservco/application-runner)
- [webservco/command](https://packagist.org/packages/webservco/command)
- [webservco/configuration](https://packagist.org/packages/webservco/configuration)
- [webservco/configuration-legacy](https://packagist.org/packages/webservco/configuration-legacy)
- [webservco/controller](https://packagist.org/packages/webservco/controller)
- [webservco/data](https://packagist.org/packages/webservco/data)
- [webservco/database](https://packagist.org/packages/webservco/database)
- [webservco/database-legacy](https://packagist.org/packages/webservco/database-legacy)
- [webservco/dependency-container](https://packagist.org/packages/webservco/dependency-container)
- [webservco/document-object-model](https://packagist.org/packages/webservco/document-object-model)
- [webservco/emitter](https://packagist.org/packages/webservco/emitter)
- [webservco/environment](https://packagist.org/packages/webservco/environment)
- [webservco/error](https://packagist.org/packages/webservco/error)
- [webservco/exception](https://packagist.org/packages/webservco/exception)
- [webservco/file](https://packagist.org/packages/webservco/file)
- [webservco/form](https://packagist.org/packages/webservco/form)
- [webservco/http](https://packagist.org/packages/webservco/http)
- [webservco/http-client](https://packagist.org/packages/webservco/http-client)
- [webservco/http-request-handler](https://packagist.org/packages/webservco/http-request-handler)
- [webservco/http-request-service](https://packagist.org/packages/webservco/http-request-service)
- [webservco/http-response-service](https://packagist.org/packages/webservco/http-response-service)
- [webservco/jsonapi](https://packagist.org/packages/webservco/jsonapi)
- [webservco/jsonapi-application](https://packagist.org/packages/webservco/jsonapi-application)
- [webservco/jwt](https://packagist.org/packages/webservco/jwt)
- [webservco/log](https://packagist.org/packages/webservco/log)
- [webservco/mail](https://packagist.org/packages/webservco/mail)
- [webservco/memory](https://packagist.org/packages/webservco/memory)
- [webservco/middleware](https://packagist.org/packages/webservco/middleware)
- [webservco/paypal](https://packagist.org/packages/webservco/paypal)
- [webservco/reflection](https://packagist.org/packages/webservco/reflection)
- [webservco/route](https://packagist.org/packages/webservco/route)
- [webservco/session](https://packagist.org/packages/webservco/session)
- [webservco/stopwatch](https://packagist.org/packages/webservco/stopwatch)
- [webservco/view](https://packagist.org/packages/webservco/view)
