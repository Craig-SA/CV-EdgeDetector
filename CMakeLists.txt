CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)
PROJECT(PCLVisualizer VERSION 0.1.0)

include(CTest)
enable_testing()

#For installations which somehow miss setting the correct PCL environmental variables
#these can be set as below
#set(PCL_DIR "/path/to/PCLConfig.cmake") #This line must come before the FIND_PACKAGE(PCL...) line.
#set(PCL_DIR "/usr/lib/x86_64-linux-gnu/cmake/pcl")

FIND_PACKAGE(PCL 1.11.1 REQUIRED)

if(PCL_FOUND)

INCLUDE_DIRECTORIES(${PCL_INCLUDE_DIRS}) #Tutorial code uses "PCL_INCLUDE_DIRS" but this is not found in PCLConfig.make
INCLUDE_DIRECTORIES(${PCL_APPS_INCLUDE_DIR}) #"PCL_APPS_INCLUDE_DIRS" IS defined in PCLConfig.make
#INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/src)
#INCLUDE_DIRECTORIES(/usr/include/pcl-1.11/)
#INCLUDE_DIRECTORIES(/usr/include/eigen3/)
#INCLUDE_DIRECTORIES(/usr/include/vtk-7.1/)

LINK_DIRECTORIES(${PCL_LIBRARY_DIRS})

ADD_DEFINITIONS(${PCL_DEFINITIONS})

set(SOURCE src/main.cpp)
ADD_EXECUTABLE (${PROJECT_NAME} ${SOURCE})   
TARGET_LINK_LIBRARIES (${PROJECT_NAME} ${PCL_LIBRARIES})


set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

endif()