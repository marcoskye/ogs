append_source_files(SOURCES)
append_source_files(SOURCES BHE)
append_source_files(SOURCES BoundaryConditions)
append_source_files(SOURCES LocalAssemblers)

add_library(HeatTransportBHE ${SOURCES})

target_link_libraries(HeatTransportBHE PUBLIC ProcessLib)
if (OGS_USE_PYTHON)
    target_link_libraries(HeatTransportBHE PRIVATE pybind11::pybind11)
endif()

if(BUILD_SHARED_LIBS)
    install(TARGETS HeatTransportBHE
            LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
target_link_libraries(HeatTransportBHE PUBLIC ProcessLib PRIVATE ParameterLib)

if(BUILD_TESTING)
    include(Tests.cmake)
endif()
