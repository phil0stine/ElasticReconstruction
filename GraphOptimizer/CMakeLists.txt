cmake_minimum_required(VERSION 2.8.3)
project(GraphOptimizer)
set(CMAKE_BUILD_TYPE RelWithDebInfo)

list(APPEND CMAKE_MODULE_PATH ${${PROJECT_NAME}_SOURCE_DIR}/cmake/Modules)

find_package(PCL 1.7 REQUIRED)
add_definitions(${PCL_DEFINITIONS})
include_directories(${PCL_INCLUDE_DIRS})

find_package(SuiteSparse REQUIRED)
include_directories(${SUITESPARSE_INCLUDE_DIRS})

find_package(Boost REQUIRED COMPONENTS graph system filesystem random program_options)
include_directories(${Boost_INCLUDE_DIRS})

set(libg2o_LIBRARIES -lg2o_core -lg2o_csparse_extension
  -lg2o_solver_cholmod -lg2o_solver_csparse -lg2o_solver_dense
  -lg2o_types_slam3d -lg2o_stuff -lcsparse -lcxsparse)

set(CMAKE_CXX_FLAGS "-std=c++11 -fpermissive")

include_directories(vertigo)
add_library(vertigo
  vertigo/edge_se3Switchable.cpp
  vertigo/edge_se3Switchable.h
  vertigo/edge_switchPrior.cpp
  vertigo/edge_switchPrior.h
  vertigo/types_g2o_robust.cpp
  vertigo/vertex_switchLinear.cpp
  vertigo/vertex_switchLinear.h
)

set(SRC_FILES GraphOptimizer.cpp OptApp.cpp)

add_executable(${PROJECT_NAME} ${SRC_FILES})
target_link_libraries(${PROJECT_NAME}
  ${PCL_LIBRARIES}
  ${Boost_LIBRARIES}
  ${libg2o_LIBRARIES}
  vertigo
)

install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION bin
)