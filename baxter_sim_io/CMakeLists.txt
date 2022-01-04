##############################################################################
# CMake
##############################################################################

cmake_minimum_required(VERSION 2.8.0)
project(baxter_sim_io)

##############################################################################
# Catkin
##############################################################################

# qt_build provides the qt cmake glue, roscpp the comms for a default talker
#find_package(catkin REQUIRED COMPONENTS qt_build roscpp baxter_core_msgs)
find_package(catkin REQUIRED COMPONENTS roscpp baxter_core_msgs)
# QT 4.x
find_package(Qt4 COMPONENTS QtCore QtGui)
# QT 5.x
find_package(Qt5 COMPONENTS Core Gui Widgets)
include_directories(${catkin_INCLUDE_DIRS})
# Use this to define what the package will export (e.g. libs, headers).
# Since the default here is to produce only a binary, we don't worry about
# exporting anything.
catkin_package(INCLUDE_DIRS include
  CATKIN_DEPENDS
  baxter_core_msgs
  INCLUDE_DIRS include
LIBRARIES ${PROJECT_NAME}
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  ${QT_INCLUDES}
)
##############################################################################
# Qt Environment
##############################################################################

# this comes from qt_build's qt-ros.cmake which is automatically
# included via the dependency call in manifest.xml

##############################################################################
# Sections
##############################################################################
include(${QT_USE_FILE})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

file(GLOB QT_FORMS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} ui/*.ui)
file(GLOB QT_RESOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} resources/*.qrc)
file(GLOB_RECURSE QT_MOC RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} FOLLOW_SYMLINKS include/baxter_sim_io/*.hpp)

if (Qt4_FOUND)
    QT4_ADD_RESOURCES(QT_RESOURCES_CPP ${QT_RESOURCES})
    QT4_WRAP_UI(QT_FORMS_HPP ${QT_FORMS})
    QT4_WRAP_CPP(QT_MOC_HPP ${QT_MOC})
elseif (Qt5_FOUND)
    QT5_ADD_RESOURCES(QT_RESOURCES_CPP ${QT_RESOURCES})
    QT5_WRAP_UI(QT_FORMS_HPP ${QT_FORMS})
    QT5_WRAP_CPP(QT_MOC_HPP ${QT_MOC})
else()
    message( FATAL_ERROR "No QT installation found, CMake will exit." )
endif()
    
##############################################################################
# Sources
##############################################################################

file(GLOB_RECURSE QT_SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} FOLLOW_SYMLINKS src/*.cpp)

##############################################################################
# Binaries
##############################################################################

add_executable(baxter_sim_io ${QT_SOURCES} ${QT_RESOURCES_CPP} ${QT_FORMS_HPP} ${QT_MOC_HPP})
if (Qt5_FOUND)
    list (APPEND QT_LIBRARIES "Qt5::Gui" "Qt5::Core" "Qt5::Widgets")
endif()
target_link_libraries(baxter_sim_io ${QT_LIBRARIES} ${ROS_LIBRARIES} ${catkin_LIBRARIES})

add_dependencies(baxter_sim_io baxter_core_msgs_gencpp)

install(TARGETS baxter_sim_io
ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(
  DIRECTORY include resources ui
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
