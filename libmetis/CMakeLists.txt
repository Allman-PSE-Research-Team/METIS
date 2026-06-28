# Add this directory for internal users.
include_directories(.)

# Find sources.
file(GLOB metis_sources *.c)

# Build libqmetis. The public C API remains METIS_* for wrapper compatibility.
add_library(qmetis_objs OBJECT ${metis_sources})
add_library(qmetis ${METIS_LIBRARY_TYPE} $<TARGET_OBJECTS:qmetis_objs>)
add_library(metis_compat ${METIS_LIBRARY_TYPE} $<TARGET_OBJECTS:qmetis_objs>)
set_target_properties(qmetis PROPERTIES OUTPUT_NAME qmetis)
set_target_properties(metis_compat PROPERTIES OUTPUT_NAME metis)
target_link_libraries(qmetis GKlib)
target_link_libraries(metis_compat GKlib)

if(METIS_INSTALL)
  install(TARGETS qmetis metis_compat
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
