cmake_minimum_required(VERSION 3.14)
project(my_project)

set(CMAKE_CXX_STANDARD 20)

set(USE_CPPUTILS ON)
set(USE_CROWCPP ON)
set(USE_GTEST ON)
set(USE_FMT OFF)
set(USE_RANGEV3 ON)
set(USE_RE2 OFF)
set(USE_JSON OFF)
set(USE_SPDLOG OFF)
set(USE_ARGPARSE OFF)
set(USE_ABSL ON)

include(cmake/ahmad1337_deps.cmake)

################################################################################
#                                   Targets                                    #
################################################################################

include(cmake/ahmad1337_utils.cmake)

###########
#  tests  #
###########

add_basic_executable(
    NAME test
    SRCS ut/test.cc
)

target_include_directories(
    test
    include/
)

link_to_all(
    TARGETS
        test
    DEPS
        cpputils::cpputils
        range-v3::range-v3
        absl::strings
        absl::str_format
        GTest::gtest
)

############
#  webapp  #
############

add_basic_executable(
    NAME app
    SRCS src/main.cc
)

target_include_directories(
    app
    include/
)

link_to_all(
    TARGETS
        app
    DEPS
        cpputils::cpputils
        range-v3::range-v3
        absl::strings
        absl::str_format
        Crow::Crow
)
