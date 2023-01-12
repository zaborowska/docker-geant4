ARG BASE_IMAGE=ubuntu:jammy
FROM $BASE_IMAGE
LABEL maintainer="anna.zaborowska@cern.ch"

ARG G4_VERSION=11.1.0

#labels
LABEL org.label-schema.geant4-version=$G4_VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.name="zaborowska/geant4"
LABEL org.label-schema.description="Geant4 Docker image"
LABEL org.label-schema.url="https://github.com/zaborowska/docker-geant4"
LABEL org.label-schema.docker.cmd="docker build -t zaborowska/geant4:latest --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') --no-cache=true ."

WORKDIR /workspace

ENV LANG=C.UTF-8
RUN ln -sf /usr/share/zoneinfo/UTC /etc/localtime
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -yq --no-install-recommends install \ 
     ca-certificates \
     dirmngr \
     gpg \
     wget \
     git \
     xauth

COPY packages packages
RUN apt-get update && \
    apt-get -yq  install \
    g++ \
    $(cat packages) \
    && \
    apt-get -y autoremove && \
    apt-get -y clean && \
    rm -rf /var/cache/apt/archives/* && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /workspace/geant4/build && \
    mkdir -p /opt/geant4/ && \
    wget --quiet -O /workspace/geant4.tar.gz \
    https://geant4-data.web.cern.ch/geant4-data/releases/source/geant4-v${G4_VERSION}.tar.gz && \
    tar xf /workspace/geant4.tar.gz -C /workspace/geant4/ && \
    mv /workspace/geant4/geant4-v${G4_VERSION}/ /workspace/geant4/src/ && \
    cd /workspace/geant4/build && \
    cmake -G Ninja -DCMAKE_INSTALL_PREFIX=/opt/geant4 \
    -DGEANT4_INSTALL_DATA=ON \
    -DGEANT4_INSTALL_DATADIR=/opt/geant4/data \
    -DGEANT4_BUILD_MULTITHREADED=ON \
    -DGEANT4_USE_GDML=ON \
    -DGEANT4_USE_QT=ON \
    -DGEANT4_USE_OPENGL_X11=OFF \
    -DGEANT4_INSTALL_EXAMPLES=ON \
    ../src/ && \
     ninja install

RUN rm packages

RUN git clone https://gitlab.cern.ch/azaborow/geant4tutorialapplication.git \
    && mkdir geant4tutorialapplication/build \
    && cmake -B geant4tutorialapplication/build -S geant4tutorialapplication \
    && cmake --build geant4tutorialapplication/build \
    && ls geant4tutorialapplication/build

COPY bashrc /etc/profile.d/custom.sh

ENTRYPOINT  ["/usr/bin/bash", "-l", "-c"]
