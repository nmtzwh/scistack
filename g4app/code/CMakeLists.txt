#----------------------------------------------------------------------------
# Setup the project
cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(g4simple)

# MPI packages
find_package(MPI REQUIRED)

#----------------------------------------------------------------------------
# Find Geant4 package, activating all available UI and Vis drivers by default
# You can set WITH_GEANT4_UIVIS to OFF via the command line or ccmake/cmake-gui
# to build a batch mode only executable
#
option(WITH_GEANT4_UIVIS "Build example with Geant4 UI and Vis drivers" ON)
if(WITH_GEANT4_UIVIS)
  find_package(Geant4 REQUIRED ui_all vis_all)
else()
  find_package(Geant4 REQUIRED)
endif()

find_package(G4mpi REQUIRED)

#----------------------------------------------------------------------------
# Setup Geant4 include directories and compile definitions
#
include(${Geant4_USE_FILE})

#----------------------------------------------------------------------------
# Find ROOT (required package)
#
find_package(ROOT REQUIRED)

#----------------------------------------------------------------------------
# Locate sources and headers for this project
#
include_directories(${Geant4_INCLUDE_DIR}
                    ${ROOT_INCLUDE_DIR}
                    ${G4mpi_INCLUDE_DIR})

#----------------------------------------------------------------------------
# Add the executable, and link it to the Geant4 libraries
#
add_executable(g4simple g4simple.cc)
target_link_libraries(g4simple ${G4mpi_LIBRARIES} ${Geant4_LIBRARIES} ${ROOT_LIBRARIES} )

#----------------------------------------------------------------------------
# Copy all scripts to the build directory, i.e. the directory in which we
# build g4simple. This is so that we can run the executable directly because it
# relies on these scripts being in the current working directory.
#
#set(g4simple_SCRIPTS
    #run.mac visualize.mac runGerda.mac
  #)

#foreach(_script ${g4simple_SCRIPTS})
  #configure_file(
    #${PROJECT_SOURCE_DIR}/${_script}
    #${PROJECT_BINARY_DIR}/${_script}
    #COPYONLY
    #)
#endforeach()

#----------------------------------------------------------------------------
# Install the executable to 'bin' directory under CMAKE_INSTALL_PREFIX
#
install(TARGETS g4simple DESTINATION bin)

