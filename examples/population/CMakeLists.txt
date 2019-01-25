SET(example_name population)

SET(KIT_SRCS
  population.cpp
  population.h
  main.cpp
  )

SET(KIT_MOC_SRCS
  population.h
  )

if(QtSOAP_QT_VERSION VERSION_LESS "5")
  QT4_WRAP_CPP(KIT_MOC_CPP ${KIT_MOC_SRCS})
else()
  qt5_wrap_cpp(KIT_MOC_CPP ${KIT_MOC_SRCS})
endif()
#QT4_WRAP_CPP(KIT_MOC_CPP ${KIT_MOC_SRCS})

INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
  )

ADD_EXECUTABLE(${example_name} ${KIT_SRCS} ${KIT_MOC_CPP})

#TARGET_LINK_LIBRARIES(${example_name} ${PROJECT_NAME})
if(QtSOAP_QT_VERSION VERSION_LESS "5")
  set(${PROJECT_NAME}_LINK_LIBRARIES ${QT_LIBRARIES})
else()
  set(${PROJECT_NAME}_LINK_LIBRARIES Qt5::Gui Qt5::Widgets Qt5::Core Qt5::Xml Qt5::Network)
endif()

message(STATUS libname)
message(STATUS ${libname})
message(STATUS ${PROJECT_NAME})
TARGET_LINK_LIBRARIES(
  ${example_name} 
  ${libname}
  ${${PROJECT_NAME}_LINK_LIBRARIES}
  ${PROJECT_NAME}
  )
