# docker-geant4

## Docker container with Geant4 for amd64 and arm64

you can download this container with:

`docker pull carlomt/geant4`

### Geant4 datasets

To keep the size of the Docker images limited, the Geant4 datasets are not installed. They are expect to be found in
`/opt/geant4/data`
I suggest you to map a folder in the host to use always the same dataset with the option:

`--volume="<GEANT4_DATASETS_PATH>:/opt/geant4/data`

The image will check the datasets at login, if some are missing install them with:

`geant4-config  --install-datasets`

### Geant4 examples

To save space, Geant4 examples have been removed, to download them:

`wget https://gitlab.cern.ch/geant4/geant4/-/archive/master/geant4-master.tar.gz?path=examples -O examples.tar.gz && tar xf examples.tar.gz --strip-components 1`
