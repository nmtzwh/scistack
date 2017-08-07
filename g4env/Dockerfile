FROM scistack/mpich:latest
ARG version="4.10.3"
LABEL description="Geant4 with MPI"
LABEL version="${version}"

# building G4mpi
RUN source /softwares/geant4/geant4.10.03-install/bin/geant4.sh && \
    source /softwares/geant4/geant4.10.03-install/share/Geant4-10.3.1/geant4make/geant4make.sh

RUN cd /softwares/geant4/geant4.10.03-install/share/Geant4-10.3.1/examples/extended/parallel/MPI && \
    mkdir build && cd build && \
    cmake -DGeant4_DIR=/softwares/geant4/geant4.10.03-install/lib64/Geant4-10.3.1 -DCMAKE_INSTALL_PREFIX=/softwares/geant4/geant4.10.03-install ../source && \
    make && make install && make clean
    
WORKDIR /root


