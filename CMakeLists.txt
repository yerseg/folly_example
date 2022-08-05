cmake_minimum_required(VERSION 3.7)

project (folly_example)
    list (APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

    find_package(Folly REQUIRED)

    set (Boost_NO_SYSTEM_PATHS ON)
    set (BOOST_ROOT "${FOLLY_ROOT_DIR}/../boost-ihLAZPV-i1fRPBpza9Ck5jOgUbrjJzx7Gh6AeYsUsC0")

    find_package(Boost 
        REQUIRED COMPONENTS 
            filesystem
            context
            program_options
            regex
            system
            thread)

    find_package(Gflags REQUIRED)
    find_package(Fmt REQUIRED)
    find_package(Threads REQUIRED)

    message(STATUS "FOLLY_ROOT_DIR = ${FOLLY_ROOT_DIR}")
    message(STATUS "FOLLY_INCLUDE_DIR = ${FOLLY_INCLUDE_DIR}")
    message(STATUS "FOLLY_LIBRARIES = ${FOLLY_LIBRARIES}")

    message(STATUS "Boost_INCLUDE_DIRS = ${Boost_INCLUDE_DIRS}")
    message(STATUS "Boost_LIBRARIES = ${Boost_LIBRARIES}")

    set(CMAKE_CXX_STANDARD 17)
    include_directories(${Boost_INCLUDE_DIRS})
    include_directories(${FOLLY_INCLUDE_DIR})

    if (NOT TARGET Folly::folly)
        include("${FOLLY_ROOT_DIR}/lib/cmake/folly/folly-targets.cmake")
    endif()

    set(FOLLY_LIBRARIES Folly::folly)

    if (NOT folly_FIND_QUIETLY)
        message(STATUS "Found folly: ${PACKAGE_PREFIX_DIR}")
    endif()

    add_executable(folly_example src/main.cpp)
    target_link_libraries(folly_example ${Boost_LIBRARIES} ${FOLLY_LIBRARIES})