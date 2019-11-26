# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

set(LIBXML2_SOURCES

        platform_external_libxml2/SAX.c
        platform_external_libxml2/entities.c
        platform_external_libxml2/encoding.c
        platform_external_libxml2/error.c
        platform_external_libxml2/parserInternals.c
        platform_external_libxml2/parser.c
        platform_external_libxml2/tree.c
        platform_external_libxml2/hash.c
        platform_external_libxml2/list.c
        platform_external_libxml2/xmlIO.c
        platform_external_libxml2/xmlmemory.c
        platform_external_libxml2/uri.c
        platform_external_libxml2/valid.c
        platform_external_libxml2/xlink.c
        platform_external_libxml2/debugXML.c
        platform_external_libxml2/xpath.c
        platform_external_libxml2/xpointer.c
        platform_external_libxml2/xinclude.c
        platform_external_libxml2/DOCBparser.c
        platform_external_libxml2/catalog.c
        platform_external_libxml2/globals.c
        platform_external_libxml2/threads.c
        platform_external_libxml2/c14n.c
        platform_external_libxml2/xmlstring.c
        platform_external_libxml2/buf.c
        platform_external_libxml2/xmlregexp.c
        platform_external_libxml2/xmlschemas.c
        platform_external_libxml2/xmlschemastypes.c
        platform_external_libxml2/xmlunicode.c
        platform_external_libxml2/xmlreader.c
        platform_external_libxml2/relaxng.c
        platform_external_libxml2/dict.c
        platform_external_libxml2/SAX2.c
        platform_external_libxml2/xmlwriter.c
        platform_external_libxml2/legacy.c
        platform_external_libxml2/chvalid.c
        platform_external_libxml2/pattern.c
        platform_external_libxml2/xmlsave.c
        platform_external_libxml2/xmlmodule.c
        platform_external_libxml2/schematron.c
        platform_external_libxml2/HTMLparser.c
        platform_external_libxml2/HTMLtree.c
        )

configure_file(xmlversion.h ${CMAKE_CURRENT_SOURCE_DIR}/platform_external_libxml2/include/libxml/xmlversion.h COPYONLY)

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
        PUBLIC platform_external_libxml2/include
        PRIVATE platform_external_libxml2)
