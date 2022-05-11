set(EXIV2_INCLUDE_PATH "${CMAKE_CURRENT_LIST_DIR}/include")
set(EXIV2_LIB_PATH "${CMAKE_CURRENT_LIST_DIR}/lib")

if (WIN32)
    set(EXIV2_LIB_PATH "${EXIV2_LIB_PATH}/win-x86_64/exiv2.lib")
elseif (APPLE)
    if (${CMAKE_SYSTEM_PROCESSOR} STREQUAL "arm64")
        set(EXIV2_LIB_PATH "${EXIV2_LIB_PATH}/macOS-arm64/libexiv2.1.0.0.9.dylib")
    else ()
        set(EXIV2_LIB_PATH "${EXIV2_LIB_PATH}/macOS-x86_64/libexiv2.1.0.0.9.dylib")
    endif ()
elseif (UNIX)
    set(EXIV2_LIB_PATH "${EXIV2_LIB_PATH}/linux-x86_64/libexiv2.so.1.0.0.9")
endif ()

add_library(exiv2 UNKNOWN IMPORTED GLOBAL)
set_target_properties(exiv2 PROPERTIES INTERFACE_INCLUDE_DIRECTORIES "${EXIV2_INCLUDE_PATH}")
set_target_properties(exiv2 PROPERTIES IMPORTED_LOCATION "${EXIV2_LIB_PATH}")

