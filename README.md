# docker-geant4

## Docker container with Geant4

you can download this container with:

NOT YET, WILL BE DONE SOON
`docker pull zaborowska/geant4`

Then run the docker container in a way that allows GUI:

`docker run -e XAUTHADD="`xauth list`" --net=host -e DISPLAY -v /tmp/.X11-unix  --name geant4 -it zaborowska/geant4 bash`

### Geant4 examples

Source code of Geant4 examples can be found in:

`/workspace/geant4/src/examples`

### Geant4 Tutorial application

Geant4 application used in Geant4 tutorial is installed in:

`/workspace/geant4tutorialapplication/build`


### Install new applications

To install any new applications run:

`apt-get update`
`apt-get install <NAME>`





