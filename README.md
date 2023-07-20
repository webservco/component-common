# webservco/component-common

Common dependencies for component projects.

---

## Component workflow

### [Create project repository](https://github.com/organizations/webservco/repositories/new)

### Set up project name

```sh
COMPONENT_NAME='COMPONENT_NAME';
```

### Run customization commands (clone `component-skeleton`)

```sh
cd ~/p/webservco && \
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
mkdir bin config public resources tests && \
cd ~/p/webservco
```

### Add code

### Development

```sh
# Customize
DOCKER_IMAGE_TAG="webservco-component-${COMPONENT_NAME}";
DOCKER_CONTAINER_NAME="webservco-component-${COMPONENT_NAME}-container";
# Build and run
docker build --tag ${DOCKER_IMAGE_TAG} -f vendor/webservco/component-common/.docker/config/php82-cli-copy/Dockerfile .
docker run -it --rm --name ${DOCKER_CONTAINER_NAME} ${DOCKER_IMAGE_TAG} /bin/bash -c "composer check:phpcs"
# Cleanup
docker image rm ${DOCKER_IMAGE_TAG}
```

### Publish tag

### [Publish on packagist](https://packagist.org/packages/submit)

---

## Index

- webservco/application
- webservco/application-default
- webservco/application-runner
- webservco/command
- webservco/component-common (Common dependencies)
- webservco/component-skeleton (Project template)
- webservco/configuration
- webservco/configuration-legacy
- webservco/controller
- webservco/data
- webservco/database
- webservco/database-legacy
- webservco/data-transfer
- webservco/dependency-container
- webservco/document-object-model
- webservco/emitter
- webservco/environment
- webservco/error
- webservco/exception
- webservco/http
- webservco/http-request-handler
- webservco/log
- webservco/middleware
- webservco/route
- webservco/stopwatch
- webservco/view
