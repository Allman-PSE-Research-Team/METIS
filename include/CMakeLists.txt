if(METIS_INSTALL)
  install(FILES metis.h DESTINATION include RENAME qmetis.h)
  install(FILES metis.h DESTINATION include)
endif()
