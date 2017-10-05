FROM scistack/g4mpi:latest
ARG version="1.0"
LABEL description="Geant4 simulation example"
LABEL version="${version}"

# manually add geant4 env
# source geant4.sh will not save env to the $USER
ENV G4INSTALL="/softwares/geant4/geant4.10.03-install"
ENV G4NEUTRONHPDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4NDL4.5" \
    G4LEDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4EMLOW6.50" \
    G4LEVELGAMMADATA="${G4INSTALL}/share/Geant4-10.3.1/data/PhotonEvaporation4.3.2" \
    G4RADIOACTIVEDATA="${G4INSTALL}/share/Geant4-10.3.1/data/RadioactiveDecay5.1.1" \
    G4NEUTRONXSDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4NEUTRONXS1.4" \
    G4PIIDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4PII1.3" \
    G4REALSURFACEDATA="${G4INSTALL}/share/Geant4-10.3.1/data/RealSurface1.0" \
    G4SAIDXSDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4SAIDDATA1.1" \
    G4ABLADATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4ABLA3.0" \
    G4ENSDFSTATEDATA="${G4INSTALL}/share/Geant4-10.3.1/data/G4ENSDFSTATE2.1"
ENV PATH="${G4INSTALL}/bin:${PATH}" \
    LD_LIBRARY_PATH="${G4INSTALL}/lib64:/softwares/CLHEP/2.3.4.4/CLHEP/lib:/usr/lib64:${LD_LIBRARY_PATH}"

# path environment
RUN mkdir /softwares/app && cd /softwares/app && mkdir bin
ENV PATH            "/softwares/app/bin:$PATH"

# add code 
# COPY and ADD not working for `docker build - < Dockerfile`
COPY code /softwares/app/g4simple/
RUN cd /softwares/app/g4simple && mkdir build && cd build && \
    CC=mpicc CXX=mpicxx cmake .. && make && cp g4simple /softwares/app/bin

# **important** compile GEANT4 MPI applications with `mpicc` and `mpicxx`, e.g. explicitly set `CC=mpicc CXX=mpicxx` before `cmake`.


