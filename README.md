# Jovo Development

This is a docker image based on `node:14` for use in local development and CI/CD pipelines. It includes the following tools:

* bash
* git
* curl
* python3
* gnupg
* make
* node 14 / npm
* jovo-cli (Jovo command line interface: `jovo [commands]`)
* ask-cli (Alexa Skills Kit command line interface: `ask [commands]`)
* gcloud ([Google Cloud SDK] command line interface: `gcloud [commands]`)
* gactions (Google Conversational Actions command line interface: `gactions [commands]` -- *as yet untested*)

[Google Cloud SDK]: https://cloud.google.com/sdk/docs/downloads-docker

## Versions

Since I expect this image to be used primarily in local development and CI/CD pipelines, I've made the Alpine-based image the default, as it should be smallest.

* `dnotes/jovo`, `dnotes/jovo:latest`, `dnotes/jovo:alpine`: the standard image, based on node:14-alpine
* (@todo) `dnotes/jovo:slim`: image based on node:14-slim
* (@todo) `dnotes/jovo:full`: image based on node:14

In future there may also be images for dealing specifically with Amazon AWS or Google Cloud backends.

## Local development

The image is set up to work in the `/app` directory as the `node` user; mounting a local directory at that location will allow you to work with your local codebase.

Since there are a number of tools, the command must be specified for each one.

* To start a new Jovo project:
  `docker run -it -v $(pwd):/app dnotes:jovo jovo new`

* To run the Jovo debugger:
  `docker run -it -v $(pwd):/app dnotes:jovo jovo run -w`

* To login to Google Cloud:
  `docker run -it -v $(pwd):/app dnotes:jovo gcloud auth login`
    * *NOTE: Completing authentication will save your Google Cloud credentials to the container's volume, and for the sake of security you should not use that volume in other containers. See the [Google Cloud SDK] documentation.*

## Continuous Integration / Deployment

@todo

## Acknowledgements

Inspired by / forked from [theBenForce: Jovo Deploy Container](https://github.com/theBenForce/jovo-deploy-container)