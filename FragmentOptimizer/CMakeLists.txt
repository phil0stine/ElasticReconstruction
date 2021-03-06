cmake_minimum_required(VERSION 2.8.3)
project(FragmentOptimizer)
set(CMAKE_BUILD_TYPE RelWithDebInfo)

list(APPEND CMAKE_MODULE_PATH ${${PROJECT_NAME}_SOURCE_DIR}/cmake/Modules)

find_package(PCL 1.7 REQUIRED)
add_definitions(${PCL_DEFINITIONS})
include_directories(${PCL_INCLUDE_DIRS})

find_package(Boost REQUIRED COMPONENTS graph system filesystem random program_options)
include_directories(${Boost_INCLUDE_DIRS})

find_package(SuiteSparse REQUIRED)
include_directories(${SUITESPARSE_INCLUDE_DIRS})

find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

set(CMAKE_CXX_FLAGS "-std=c++11 -fpermissive")

set(SRC_FILES FragmentOptimizer.cpp HashSparseMatrix.cpp OptApp.cpp PointCloud.cpp)

add_executable(${PROJECT_NAME} ${SRC_FILES})
target_link_libraries(${PROJECT_NAME}
  ${PCL_LIBRARIES}
  ${Boost_LIBRARIES}
  ${SUITESPARSE_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION bin
)