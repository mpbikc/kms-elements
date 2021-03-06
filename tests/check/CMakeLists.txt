include_directories(
  ${gstreamer-1.5_INCLUDE_DIRS}
  ${gstreamer-video-1.5_INCLUDE_DIRS}
  ${CMAKE_CURRENT_SOURCE_DIR}
)

set(KMS_TEST_UTILS_SOURCES
  kmstestutils.h kmstestutils.c
  )

add_library(kmstestutils ${KMS_TEST_UTILS_SOURCES})

target_link_libraries(kmstestutils
  ${gstreamer-1.5_LIBRARIES}
  ${gstreamer-base-1.5_LIBRARIES}
  ${gstreamer-sdp-1.5_LIBRARIES}
  ${gstreamer-pbutils-1.5_LIBRARIES}
)

include (TestHelpers)

set (SUPPRESSIONS "${CMAKE_CURRENT_SOURCE_DIR}/valgrind.supp")

set (TEST_PROPERTIES
  GST_PLUGIN_PATH=$ENV{GST_PLUGIN_PATH}:${CMAKE_PREFIX_PATH}:${CMAKE_BINARY_DIR}
  CK_DEFAULT_TIMEOUT=50
  )

set (VALGRING_TEST_PROPERTIES
  ${TEST_PROPERTIES}
  CK_DEFAULT_TIMEOUT=1000
  )


add_subdirectory(element)

# if (${ENABLE_INTEGRATION_TESTS})
#   add_subdirectory(integration)
# endif()

# if (${ENABLE_MEMORY_LEAKS_TESTS})
#   add_subdirectory(memory_leaks)
# endif()
