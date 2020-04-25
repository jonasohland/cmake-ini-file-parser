cmake_minimum_required(VERSION 3.9)
project(INIFileParser)

set(INIFileParser_CONFIG_TEMPLATE       "${CMAKE_CURRENT_LIST_DIR}/templates/INIFileParser-config.cmake.in")
set(INIFileParser_CONFIG_FILE           "${CMAKE_CURRENT_BINARY_DIR}/INIFileParser-config.cmake")
set(INIFileParser_VERSION_FILE          "${CMAKE_CURRENT_BINARY_DIR}/INIFileParser-version.cmake")


set(_ifp_version                        0.0.1)
set(_ifp_module_path                    "${CMAKE_CURRENT_LIST_DIR}/cmake")
set(_ifp_module                         "${_ifp_module_path}/INIFileParser.cmake")

set(INIFileParser_INSTALL_LOCATION      "lib/INIFileParser-${_ifp_version}")

get_directory_property(_has_parent_scope PARENT_DIRECTORY)

if(_has_parent_scope)

    set(INIFileParser_VERSION           "${_ifp_version}"       PARENT_SCOPE)
    set(INIFileParser_ModulePath        "${_ifp_module_path}"   PARENT_SCOPE)
    set(INIFileParser_Module            "${_ifp_module}"        PARENT_SCOPE)

else()

    set(INIFileParser_VERSION           ${_ifp_version})
    
    include(CMakePackageConfigHelpers)

    configure_file(
        "${INIFileParser_CONFIG_TEMPLATE}"
        "${INIFileParser_CONFIG_FILE}"
        @ONLY)

    write_basic_package_version_file(
        ${INIFileParser_VERSION_FILE}
        VERSION ${INIFileParser_VERSION}
        COMPATIBILITY SameMajorVersion)

    install(
        FILES 
            "${INIFileParser_CONFIG_FILE}"
            "${INIFileParser_VERSION_FILE}"
        DESTINATION
            "${INIFileParser_INSTALL_LOCATION}")

    install(
        FILES
            "${_ifp_module}"
        DESTINATION
            "${INIFileParser_INSTALL_LOCATION}/cmake"
    )

endif()
