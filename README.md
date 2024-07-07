# webservco/component-common

Common dependencies for component projects.

---

## Component workflow

### [Create project repository](https://github.com/organizations/webservco/repositories/new)

- public
- do not check anything else (no README, etc, make sure repo will be empty initially).

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
rm -f src/WebServCo/.gitignore && git add src/WebServCo && git commit -m 'Init src' && \
printf '%s\n' "# webservco/$COMPONENT_NAME" '' 'A PHP component/library.' '' '---' > README.md && \
sed -i -e "s|\"name\" : \"webservco/component-skeleton\"|\"name\" : \"webservco/$COMPONENT_NAME\"|g" composer.json && \
git add README.md && \
git add composer.json && \
git commit -m 'Customize' && \
git push -u origin main && \
mkdir bin config public resources tests
```

### Add code

### Development

Only useful if can not provide environment on local, otherwise it is more complex to work in this way.

```sh
# Customize
DOCKER_IMAGE_TAG="webservco-component-${COMPONENT_NAME}";
DOCKER_CONTAINER_NAME="webservco-component-${COMPONENT_NAME}-container";

# Download Docker configuration
svn export --force https://github.com/webservco/component-common.git/trunk/.docker

# Build and run
docker build --tag ${DOCKER_IMAGE_TAG} -f .docker/config/php83-cli-copy/Dockerfile .
docker run -it --rm --name ${DOCKER_CONTAINER_NAME} ${DOCKER_IMAGE_TAG} /bin/bash -c "composer check:phpcs"

# Cleanup
docker image rm ${DOCKER_IMAGE_TAG}
```

### Add dependencies

### Publish tag

### [Publish on packagist](https://packagist.org/packages/submit)

### Update index

---

## Index

- [webservco/application](https://packagist.org/packages/webservco/application)
- [webservco/application-default](https://packagist.org/packages/webservco/application-default)
- [webservco/application-runner](https://packagist.org/packages/webservco/application-runner)
- [webservco/command](https://packagist.org/packages/webservco/command)
- [webservco/component-common (Common dependencies)](https://packagist.org/packages/webservco/component-common)
- webservco/component-skeleton (Project template, not on packagist)
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
