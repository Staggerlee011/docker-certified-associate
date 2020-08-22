# Describe options, such as add, copy, volumes, expose, entry point

Below are the building blocks for creating a dockerfile. 

## Comments

comments are written using `#`

`# This is a comment`

## FROM

Starting point for a dockerfile, used to pull from other images.

You can either use:

`FROM alpine`

which will get the verison of alpine tagged with latest (Tagging with latest is done manually so may not actually be the most up to date version!)

`FROM alpine:3.5`

Which will bring a specific verison (This is prefered method in production! as latest could bring instability)

## ADD

## COPY

Copies a file or files during thje build

`COPY . /src`

copies everything in the current folder to the src folder in the docker image

## ENV

Sets environment variables within the container, useful for setting vars within the container that applicaitons will need

`ENV`

## EXPOSE

Publishes a port to external systems

`EXPOSE 8080`

## LABEL

simple metadata option to add reference and detail to your image

`LABEL maintainer="stebennettsjb@gmail.com"
LABEL version=1.0
LABEL description="This is a image for foo"`

you can alsohave multiple labels on a single row (Used to save space but doesnt since 1.10)

`LABEL multi.label1="value1" muti.label2="value2"`

## STOPSIGNAL

## USER

## VOLUME

Exposes a path to the file system outside of the container, This can be used for example to do a restore of database

`VOLUME`

## WORKDIR

Defines the working directory to use, normally used in conjuntion with run to ensure you are in the correct directory for the exe

## RUN

Runs command in the container

`RUN apk add --update nodejs nodejs-npm`

## ENTRYPOINT

Defines what application in the container are open to use

`ENTRYPOINT ["node", "./app.js"]`
