#
# Copyright (C) 2020 Intel Corporation
#
# SPDX-License-Identifier: MIT
#

set(TARGET_NAME ${TARGET_NAME_L0}_mocks)

set(L0_MOCKS_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/CMakeLists.txt
    ${CMAKE_CURRENT_SOURCE_DIR}/debugger_l0_create.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_built_ins.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_built_ins.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_cmdlist.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_cmdlist.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_cmdqueue.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_cmdqueue.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_context.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_device.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_device.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_driver.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_driver.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_driver_handle.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_driver_handle.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_event.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_event.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_gmm_resource_info_l0.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_kernel.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_l0_debugger.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_memory_manager.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_module.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_module.h
    ${CMAKE_CURRENT_SOURCE_DIR}/mock_sampler.h
)

add_library(${TARGET_NAME} OBJECT ${L0_MOCKS_SOURCES})

target_include_directories(${TARGET_NAME} PRIVATE
                           $<TARGET_PROPERTY:gmock-gtest,INTERFACE_INCLUDE_DIRECTORIES>
                           $<TARGET_PROPERTY:${L0_MOCKABLE_LIB_NAME},INTERFACE_INCLUDE_DIRECTORIES>
                           $<TARGET_PROPERTY:${NEO_SHARED_MOCKABLE_LIB_NAME},INTERFACE_INCLUDE_DIRECTORIES>
                           ${NEO_SOURCE_DIR}/level_zero/core/test/unit_test
)

target_compile_definitions(${TARGET_NAME} PUBLIC $<TARGET_PROPERTY:${L0_MOCKABLE_LIB_NAME},INTERFACE_COMPILE_DEFINITIONS>)
set_target_properties(${TARGET_NAME} PROPERTIES FOLDER ${TARGET_NAME_L0})

create_source_tree(${TARGET_NAME} ${L0_ROOT_DIR})
