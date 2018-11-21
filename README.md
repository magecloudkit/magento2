# MageCloudKit Magento 2 Docker Image

Magento 2 Docker Image for MageCloudKit.

## Building the Docker images locally

    $ docker build --rm=false -t magecloudkit/magento2:latest magento
    $ docker build --rm=false -t magecloudkit/nginx:${BUILD_NUM} ./docker/nginx

## Building the Docker images on CircleCI

This repository includes a sample configuration file for building MageCloudKit Docker images using
[CircleCI](https://circleci.com).

As the database is not available on CircleCI, we need to need to include a Magento configuration file
(`magento/app/etc/config.php`). This allows the Magento to correctly discovered the enabled modules and
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
