FROM scistack/clhep:latest
ARG version="4.10.3"
LABEL description="GEANT4 simulation package"
LABEL version="${version}"

# building clhep
RUN mkdir /softwares/geant4 

RUN yum update -y && \
    yum -y install xerces-c-devel libX11-devel mesa-libGL-devel qt-devel motif-devel && \
    yum -y clean all
    
RUN wget http://geant4.web.cern.ch/geant4/support/source/geant4.10.03.p01.tar.gz -O /var/tmp/geant4.10.03.p01.tar.gz && \
    tar zxf /var/tmp/geant4.10.03.p01.tar.gz -C /softwares/geant4 && rm /var/tmp/geant4.10.03.p01.tar.gz

RUN mkdir /softwares/geant4/geant4.10.03-install && mkdir /softwares/geant4/geant4.10.03.p01/build
WORKDIR /softwares/geant4/geant4.10.03.p01/build

RUN cmake -DCMAKE_INSTALL_PREFIX=/softwares/geant4/geant4.10.03-install \
          -DCMAKE_BUILD_TYPE=RelWithDebInfo \
          -DGEANT4_INSTALL_DATA=ON \
          -DCLHEP_ROOT_DIR=/softwares/CLHEP/2.3.4.4/CLHEP \
          -DGEANT4_USE_OPENGL_X11=ON \
          -DGEANT4_USE_RAYTRACER_X11=ON \
          -DGEANT4_USE_GDML=ON \
          -DGEANT4_USE_QT=ON \
          /softwares/geant4/geant4.10.03.p01 && \
    make && make install && \
    rm -rf /softwares/geant4/geant4.10.03.p01


    
