# docker-geant4

## Docker container with Geant4

you can download this container with:

NOT YET, WILL BE DONE SOON
`docker pull zaborowska/geant4`

### Geant4 examples

Source code of Geant4 examples can be found in:

`/workspace/geant4/src/examples`

### Geant4 Tutorial application

Geant4 application used in Geant4 tutorial is installed in:

`/workspace/geant4tutorialapplication/build`

### Use graphics interface

To use any GUI application (not only Geant4 visualisation), run on your host machine:

`xauth list`

Copy the complete output (3 strings).

Then run the docker container in a way that allows GUI, run:

`docker run  --net=host -e DISPLAY -v /tmp/.X11-unix  --name geant4 -it zaborowska/geant4 bash`

and then use the previously copied output:

`xauth add <OUTPUT OF xauth list ON HOST MACHINE>`

### Install new applications

To install any new applications run:

`apt-get update`
`apt-get install <NAME>`





