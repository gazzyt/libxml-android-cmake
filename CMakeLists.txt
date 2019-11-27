# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules" )

include(DownloadProject)
download_project(
	PROJ			platform_external_libxml2
	GIT_REPOSITORY  https://github.com/aosp-mirror/platform_external_libxml2.git
	GIT_TAG         platform-tools-29.0.5
)

set(LIBXML2_SOURCES

        ${platform_external_libxml2_SOURCE_DIR}/SAX.c
        ${platform_external_libxml2_SOURCE_DIR}/entities.c
        ${platform_external_libxml2_SOURCE_DIR}/encoding.c
        ${platform_external_libxml2_SOURCE_DIR}/error.c
        ${platform_external_libxml2_SOURCE_DIR}/parserInternals.c
        ${platform_external_libxml2_SOURCE_DIR}/parser.c
        ${platform_external_libxml2_SOURCE_DIR}/tree.c
        ${platform_external_libxml2_SOURCE_DIR}/hash.c
        ${platform_external_libxml2_SOURCE_DIR}/list.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlIO.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlmemory.c
        ${platform_external_libxml2_SOURCE_DIR}/uri.c
        ${platform_external_libxml2_SOURCE_DIR}/valid.c
        ${platform_external_libxml2_SOURCE_DIR}/xlink.c
        ${platform_external_libxml2_SOURCE_DIR}/debugXML.c
        ${platform_external_libxml2_SOURCE_DIR}/xpath.c
        ${platform_external_libxml2_SOURCE_DIR}/xpointer.c
        ${platform_external_libxml2_SOURCE_DIR}/xinclude.c
        ${platform_external_libxml2_SOURCE_DIR}/DOCBparser.c
        ${platform_external_libxml2_SOURCE_DIR}/catalog.c
        ${platform_external_libxml2_SOURCE_DIR}/globals.c
        ${platform_external_libxml2_SOURCE_DIR}/threads.c
        ${platform_external_libxml2_SOURCE_DIR}/c14n.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlstring.c
        ${platform_external_libxml2_SOURCE_DIR}/buf.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlregexp.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlschemas.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlschemastypes.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlunicode.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlreader.c
        ${platform_external_libxml2_SOURCE_DIR}/relaxng.c
        ${platform_external_libxml2_SOURCE_DIR}/dict.c
        ${platform_external_libxml2_SOURCE_DIR}/SAX2.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlwriter.c
        ${platform_external_libxml2_SOURCE_DIR}/legacy.c
        ${platform_external_libxml2_SOURCE_DIR}/chvalid.c
        ${platform_external_libxml2_SOURCE_DIR}/pattern.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlsave.c
        ${platform_external_libxml2_SOURCE_DIR}/xmlmodule.c
        ${platform_external_libxml2_SOURCE_DIR}/schematron.c
        ${platform_external_libxml2_SOURCE_DIR}/HTMLparser.c
        ${platform_external_libxml2_SOURCE_DIR}/HTMLtree.c
        )


configure_file(xmlversion.h ${platform_external_libxml2_SOURCE_DIR}/include/libxml/xmlversion.h COPYONLY)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
        libxml2

        # Sets the library as a shared library.
        STATIC

        # Provides a relative path to your source file(s).
        ${LIBXML2_SOURCES})

target_compile_definitions(libxml2 PUBLIC STATIC_LIBXML LIBXML_THREAD_ENABLED=1)

target_include_directories(libxml2
        PUBLIC ${platform_external_libxml2_SOURCE_DIR}/include
        PRIVATE ${platform_external_libxml2_SOURCE_DIR})
