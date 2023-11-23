# Copyright 2018 Mike Dev
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at http://www.boost.org/LICENSE_1_0.txt

if(NOT DEFINED IDF_TARGET)

cmake_minimum_required(VERSION 3.5...3.20)
project(boost_array VERSION "${BOOST_SUPERPROJECT_VERSION}" LANGUAGES CXX)

add_library(boost_array INTERFACE)
add_library(Boost::array ALIAS boost_array)

target_include_directories(boost_array INTERFACE include)

target_link_libraries(boost_array
    INTERFACE
        Boost::assert
        Boost::config
        Boost::core
        Boost::static_assert
        Boost::throw_exception
)

else()

FILE(GLOB_RECURSE headers include/*.h include/*.hpp)

idf_component_register(
    SRCS
        ${headers}
    INCLUDE_DIRS
        include
    REQUIRES
        boost_assert
        boost_config
        boost_core
        boost_static_assert
        boost_throw_exception
)

endif()
