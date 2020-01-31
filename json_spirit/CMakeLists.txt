CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

SET(JSON_SPIRIT_SRCS
  json_spirit_reader.cpp json_spirit_reader.h
  json_spirit_value.cpp json_spirit_value.h
  json_spirit_writer.cpp json_spirit_writer.h
  json_spirit.h
  json_spirit_error_position.h
  json_spirit_reader_template.h
  json_spirit_stream_reader.h
  json_spirit_utils.h
  json_spirit_writer_options.h
  json_spirit_writer_template.h )
 
FIND_PACKAGE(Boost REQUIRED)
INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIR})

ADD_LIBRARY(json_spirit STATIC ${JSON_SPIRIT_SRCS})

# default install directory
if (CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set(CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_LIST_DIR}/../../packages/json_spirit" CACHE PATH "default install path" FORCE)
endif()
# install targets
install(
    TARGETS json_spirit
    EXPORT json_spirit-config
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
# install config for export group
install(
    EXPORT json_spirit-config
    DESTINATION "${CMAKE_INSTALL_PREFIX}/cmake"
)

#export includes
install(
  DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  FILES_MATCHING PATTERN "*.h"
) 