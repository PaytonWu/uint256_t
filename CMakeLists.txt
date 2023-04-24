cmake_minimum_required(VERSION 3.22)

project(
    UINT256_T
    VERSION 0.1.0
    DESCRIPTION "An unsigned 128 bit integer type for C++"
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(UINT256_LIBRARY UINT256)

if ("${CMAKE_CXX_COMPILER_ID}" MATCHES "MSVC")
    add_compile_options(
        /Zc:__cplusplus       # https://learn.microsoft.com/en-us/cpp/build/reference/zc-cplusplus
        /Zc:enumTypes         # https://learn.microsoft.com/en-us/cpp/build/reference/zc-enumtypes
        /Zc:externC           # https://learn.microsoft.com/en-us/cpp/build/reference/zc-externc
        /Zc:externConstexpr   # https://learn.microsoft.com/en-us/cpp/build/reference/zc-externconstexpr
        /Zc:inline            # https://learn.microsoft.com/en-us/cpp/build/reference/zc-inline-remove-unreferenced-comdat
        /Zc:preprocessor      # https://learn.microsoft.com/en-us/cpp/build/reference/zc-preprocessor
        /Zc:referenceBinding  # https://learn.microsoft.com/en-us/cpp/build/reference/zc-referencebinding-enforce-reference-binding-rules
        /Zc:rvalueCast        # https://learn.microsoft.com/en-us/cpp/build/reference/zc-rvaluecast-enforce-type-conversion-rules
        /Zc:strictStrings     # https://learn.microsoft.com/en-us/cpp/build/reference/zc-strictstrings-disable-string-literal-type-conversion
        /Zc:templateScope     # https://learn.microsoft.com/en-us/cpp/build/reference/zc-templatescope
        /Zc:ternary           # https://learn.microsoft.com/en-us/cpp/build/reference/zc-ternary
        /Zc:throwingNew       # https://learn.microsoft.com/en-us/cpp/build/reference/zc-throwingnew-assume-operator-new-throws
        /permissive-          # https://blogs.msdn.microsoft.com/vcblog/2016/11/16/permissive-switch/
                              # https://blogs.msdn.microsoft.com/vcblog/2017/09/11/two-phase-name-lookup-support-comes-to-msvc/
                              # https://learn.microsoft.com/en-us/cpp/build/reference/permissive-standards-conformance
        /volatile:iso         # https://learn.microsoft.com/en-us/cpp/build/reference/volatile-volatile-keyword-interpretation
        /GS
        /Zi
        /EHsc
        /fp:precise
        /errorReport:prompt
        /diagnostics:caret    # https://learn.microsoft.com/en-us/cpp/build/reference/diagnostics-compiler-diagnostic-options
        /utf-8                # https://learn.microsoft.com/en-us/cpp/build/reference/utf-8-set-source-and-executable-character-sets-to-utf-8
        /WL                   # https://learn.microsoft.com/en-us/cpp/build/reference/wl-enable-one-line-diagnostics
    )
endif()

add_library(${UINT256_LIBRARY} INTERFACE)
target_include_directories(${UINT256_LIBRARY} INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/third_party/uint128_t/include)

if (WITH_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()

install(
    TARGETS ${UINT256_LIBRARY}
    COMPONENT devel
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    DIRECTORY include
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    COMPONENT devel
)
