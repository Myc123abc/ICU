cmake_minimum_required(VERSION 3.30)
project(icu)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

###############################################################################
#                               Dependencies
###############################################################################

################################### ICU #######################################

set(ICU_VERSION 78.3)
set(ICU_URL "https://github.com/unicode-org/icu/releases/download/release-${ICU_VERSION}/icu4c-${ICU_VERSION}-Win64-MSVC2022.zip")
set(ICU_ARCHIVE "${CMAKE_SOURCE_DIR}/vendor/icu-${ICU_VERSION}.zip")
set(ICU_SOURCE_DIR "${CMAKE_SOURCE_DIR}/vendor/icu-${ICU_VERSION}")

if(NOT EXISTS "${ICU_SOURCE_DIR}")
  file(MAKE_DIRECTORY "${ICU_SOURCE_DIR}")

  message(STATUS "Downloading ICU ${ICU_VERSION}...")

  file(DOWNLOAD
    "${ICU_URL}"
    "${ICU_ARCHIVE}"
    SHOW_PROGRESS
    STATUS ICU_DOWNLOAD_STATUS
    TLS_VERIFY ON
  )

  list(GET ICU_DOWNLOAD_STATUS 0 ICU_DOWNLOAD_RESULT)
  if(NOT ICU_DOWNLOAD_RESULT EQUAL 0)
    message(FATAL_ERROR "Failed to download ICU: ${ICU_DOWNLOAD_STATUS}")
  endif()

  message(STATUS "Extracting ICU...")

  execute_process(
    COMMAND
      "${CMAKE_COMMAND}" -E tar xf "${ICU_ARCHIVE}" --format=zip
    WORKING_DIRECTORY "${ICU_SOURCE_DIR}"
    RESULT_VARIABLE ICU_EXTRACT_RESULT
  )

  if (NOT ICU_EXTRACT_RESULT EQUAL 0)
    message(FATAL_ERROR "Failed to extract ICU")
  endif()

  file(REMOVE "${ICU_ARCHIVE}")
endif()

function(target_link_icu target lib)
  target_link_libraries(${target}
    PRIVATE
      ${ICU_SOURCE_DIR}/lib64/${lib}.lib
  )
endfunction()

file(GLOB ICU_DLLS "${ICU_SOURCE_DIR}/bin64/*.dll")

function(target_copy target)
  add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
      ${ARGN}
      "$<TARGET_FILE_DIR:${target}>"
    COMMAND_EXPAND_LISTS
  )
endfunction()

###############################################################################
#                               Executable
###############################################################################

add_executable(icu main.cpp)
target_include_directories(icu
  PRIVATE
    ${ICU_SOURCE_DIR}/include
)
target_link_icu(icu icuuc)
target_copy(icu ${ICU_DLLS})
