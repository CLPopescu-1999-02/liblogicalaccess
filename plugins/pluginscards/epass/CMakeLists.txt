cmake_minimum_required(VERSION 2.6)
project(epasscards)

if (WIN32)
    SET(VERSION_PRODUCTNAME_VALUE "epasscards")
    add_definitions(-DVERSION_PRODUCTNAME_VALUE="${VERSION_PRODUCTNAME_VALUE}")
endif()

file(GLOB_RECURSE SRCS *.cpp)
file(GLOB_RECURSE INCLUDE *.hpp)

add_library(
        epasscards
        SHARED

        ${SRCS}
        ${INCLUDE}
        ${resourcerc}
)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../../pluginsreaderproviders/iso7816)

SET_TARGET_PROPERTIES(epasscards PROPERTIES VERSION ${LIBLOGICALACCESS_VERSION_STRING})

target_link_libraries(
        epasscards
        iso7816readers
        iso7816cards
        ${LIBLOGICALACCESS_LIBRARY}
)

install ( FILES ${INCLUDE} DESTINATION include/logicalaccess/plugins/cards/epass )
install ( TARGETS epasscards RUNTIME DESTINATION bin/${LIB_SUFFIX} ARCHIVE DESTINATION lib/${LIB_SUFFIX} LIBRARY DESTINATION lib/${LIB_SUFFIX} )
