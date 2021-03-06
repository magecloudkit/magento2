# MageCloudKit Magento 2 Docker Image

Magento 2 Docker Image for MageCloudKit.

This Docker image must be built locally or on a CI system with the Magento authentication keys available.
It is not a Docker Hub automated build. For more information, please see:
https://devdocs.magento.com/guides/v2.2install-gde/prereq/connect-auth.html.

## Building the Docker image locally

    $ composer global config http-basic.repo.magento.com $MAGENTO_PUBLIC_KEY $MAGENTO_PRIVATE_KEY
    $ composer install --ignore-platform-reqs
    $ docker build --rm=false -t magecloudkit/magento2:latest .
    $ docker login --username=robmorgan
    $ docker push magecloudkit/magento2:latest

## Building the Docker image on CircleCI

This repository includes a sample configuration file for building the MageCloudKit Magento 2
Docker image using [CircleCI](https://circleci.com).

As we do not have access to the database on CircleCI, we need to need to include a Magento configuration file
(`app/etc/config.php`). This allows the Magento to correctly discovered the enabled modules and
build the static assets accordingly.

### Configuring CircleCI

In order to build the Docker images on CircleCI you must set the following environment variables:

 * `MAGENTO_PUBLIC_KEY`
 * `MAGENTO_PRIVATE_KEY`

 You can download these keys from the [Magento](https://magento.com) website under 'My Account'.

If you wish to push the images to an Amazon ECR repository you must configure these additional variables:

 * `AWS_REGION`: e.g: `us-east-1`
 * `AWS_ACCESS_KEY_ID`: e.g: `xyz`
 * `AWS_SECRET_ACCESS_KEY`: e.g: `xyz`
 * `AWS_ECR_URL`: e.g: `123456789012.dkr.ecr.us-east-1.amazonaws.com/kiwico`

**Note:** Be sure to edit the CircleCI configuration file (`.circleci/config/yml`) and replace the
`us-east-1` value with your desired AWS region.

## Contributing

Users are welcome to submit issues and pull requests.
