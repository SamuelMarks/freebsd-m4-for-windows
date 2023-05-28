get_filename_component(EXEC_NAME "${CMAKE_CURRENT_SOURCE_DIR}" NAME)

set(Header_Files "parser.h")
source_group("Header Files" FILES "${Header_Files}")
# main.c
set(Source_Files "eval.c" "expr.c" "look.c" "misc.c" "gnum4.c" "trace.c" "main.c")
source_group("Source Files" FILES "${Source_Files}")

include(FindFLEX)
include(FindBISON)
find_package(BISON)
find_package(FLEX)
BISON_TARGET(MyParser parser.y ${CMAKE_CURRENT_BINARY_DIR}/parser.c)
FLEX_TARGET(MyScanner tokenizer.l  ${CMAKE_CURRENT_BINARY_DIR}/lexer.c)
ADD_FLEX_BISON_DEPENDENCY(MyScanner MyParser)

list(APPEND Source_Files ${BISON_MyParser_OUTPUTS} ${FLEX_MyScanner_OUTPUTS})

add_executable("${EXEC_NAME}" "${Header_Files}" "${Source_Files}")

include("${CMAKE_SOURCE_DIR}/cmake/modules/FindPCRE2.cmake")
message(STATUS "PCRE2_FOUND	 = ${PCRE2_FOUND}")
if (NOT PCRE2_FOUND)
    message(FATAL_ERROR "Could not find regex library")
endif ()
include(GNUInstallDirs)
target_include_directories(
        "${EXEC_NAME}"
        PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
        "$<BUILD_INTERFACE:${CMAKE_BINARY_DIR}>"
        "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)
target_link_libraries("${EXEC_NAME}" "ohash" "strtonum")

set_target_properties(
        "${EXEC_NAME}"
        PROPERTIES
        LINKER_LANGUAGE
        C
)

#include(GenerateExportHeader)
#set(_export_file "${CMAKE_BINARY_DIR}/${EXEC_NAME}_export.h")
#generate_export_header("${EXEC_NAME}" EXPORT_FILE_NAME "${_export_file}")

#################
# Install rules #
#################

# setup the version numbering
set_property(TARGET "${EXEC_NAME}" PROPERTY VERSION "${${PROJECT_NAME}_VERSION}")
set_property(TARGET "${EXEC_NAME}" PROPERTY SOVERSION "${${PROJECT_NAME}_VERSION_MAJOR}")
