# ------------------------------------------------------------------------------------------------ #
#                                This file is part of CosmoScout VR                                #
#       and may be used under the terms of the MIT license. See the LICENSE file for details.      #
#                         Copyright: (c) 2019 German Aerospace Center (DLR)                        #
# ------------------------------------------------------------------------------------------------ #

# build library ------------------------------------------------------------------------------------

file(GLOB SOURCE_FILES *.cpp */*.cpp)

# Header files are only added in order to make them available in your IDE.
file(GLOB HEADER_FILES *.hpp */*.hpp)

add_library(cs-gui SHARED
  ${SOURCE_FILES}
  ${HEADER_FILES}
)

target_link_libraries(cs-gui
  PUBLIC
    cef::cef
    cef::wrapper
    cs-utils
)

if(COSMOSCOUT_USE_PRECOMPILED_HEADERS)
  target_precompile_headers(cs-gui PRIVATE precompiled.pch)
endif()

# Make directory structure available in your IDE.
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" PREFIX "src" FILES
  ${SOURCE_FILES} ${HEADER_FILES}
)

# install the library ------------------------------------------------------------------------------

install(TARGETS cs-gui DESTINATION lib)

# export header ------------------------------------------------------------------------------------

generate_export_header(cs-gui
  EXPORT_FILE_NAME cs_gui_export.hpp
)
