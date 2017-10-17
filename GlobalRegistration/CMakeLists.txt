cmake_minimum_required(VERSION 2.8.3)
project(GlobalRegistration)
set(CMAKE_BUILD_TYPE RelWithDebInfo)


find_package(PCL 1.7 REQUIRED)
add_definitions(${PCL_DEFINITIONS})
include_directories(${PCL_INCLUDE_DIRS})

set(CMAKE_CXX_FLAGS "-std=c++11 -fpermissive")

set(SRC_FILES GlobalRegistration.cpp RansacCurvature.cpp)

add_executable(${PROJECT_NAME} ${SRC_FILES})
target_link_libraries(${PROJECT_NAME}
  ${PCL_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION bin
)