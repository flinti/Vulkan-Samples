# Copyright (c) 2023-2024, Sascha Willems
#
# SPDX-License-Identifier: Apache-2.0
#
# Licensed under the Apache License, Version 2.0 the "License";
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
 
if (NOT APPLE)
    # Not enabled on Apple platforms, as OpenCL has been deprecated on that platform

    get_filename_component(FOLDER_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)
    get_filename_component(PARENT_DIR ${CMAKE_CURRENT_LIST_DIR} PATH)
    get_filename_component(CATEGORY_NAME ${PARENT_DIR} NAME)

    add_sample_with_tags(
        ID ${FOLDER_NAME}
        CATEGORY ${CATEGORY_NAME}
        AUTHOR "Sascha Willems"
        NAME "OpenCL Interoperability"
        DESCRIPTION "Example showing sharing resources between OpenCL and Vulkan using cross vendor extensions"
        LIBS opencl
        FILES
            ../open_cl_common/open_cl_functions.inl
            ../open_cl_common/open_cl_utils.h
            ../open_cl_common/open_cl_utils.cpp
        SHADER_FILES_GLSL
            open_cl_interop/glsl/texture_display.vert
            open_cl_interop/glsl/texture_display.frag
            # Also add the OpenCL kernel so it cean be opened from the IDE
            open_cl_interop/procedural_texture.cl
        SHADER_FILES_HLSL
            open_cl_interop/hlsl/texture_display.vert.hlsl
            open_cl_interop/hlsl/texture_display.frag.hlsl)
endif()