include_directories(
    .
    ${BLASR_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
    ${HDF5_INCLUDE_DIRS}
    ${HTSLIB_INCLUDE_DIRS}
    ${PacBioBAM_INCLUDE_DIRS}
    ${PBDATA_INCLUDE_DIRS}
    ${PBDATA_ROOT_DIR}
    ${PBIHDF_INCLUDE_DIRS}
    ${ZLIB_INCLUDE_DIRS}
)

set(SOURCES
    Settings.h
    Settings.cpp
    Converter.h
    Converter.cpp
    Bam2BaxInternal.h
    RegionTypeAdapter.h
    RegionsAdapter.h
    Bam2BaxConverter.h
    Bam2BaxConverterImpl.hpp
    Bam2Bax.h
    Bam2Bax.cpp
    OptionParser.h
    OptionParser.cpp
    MetadataWriter.h
    MetadataWriter.cpp
)

set(BAM2BAX_SOURCES
    Bam2BaxMain.cpp
    ${SOURCES}
)

set(BAM2PLX_SOURCES
    Bam2PlxMain.cpp
    ${SOURCES}
)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Bam2Bax_CXX_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${Bam2Bax_EXE_LINKER_FLAGS}")

add_executable(bam2bax ${BAM2BAX_SOURCES})
set_target_properties(bam2bax PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${Bam2Bax_BinDir}
)
if (NOT APPLE)
    set(MY_LIBRT -lrt)
else()
endif()
target_link_libraries(bam2bax
    ${PBBAM_LINK_FLAG}
    ${BLASR_LIBRARIES}
    ${PBIHDF_LIBRARIES}
    ${PBDATA_LIBRARIES}
    ${HDF5_CPP_LIBRARIES}
    ${HDF5_LIBRARIES}
    ${PacBioBAM_LIBRARIES}
    ${HTSLIB_LIBRARIES}
    ${ZLIB_LIBRARIES}
    ${MY_LIBRT}
)

add_executable(bam2plx ${BAM2PLX_SOURCES} )
set_target_properties(bam2plx PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${Bam2Bax_BinDir}
)
target_link_libraries(bam2plx
    ${PBBAM_LINK_FLAG}
    ${BLASR_LIBRARIES}
    ${PBIHDF_LIBRARIES}
    ${PBDATA_LIBRARIES}
    ${HDF5_CPP_LIBRARIES}
    ${HDF5_LIBRARIES}
    ${PacBioBAM_LIBRARIES}
    ${HTSLIB_LIBRARIES}
    ${ZLIB_LIBRARIES}
    ${MY_LIBRT}
)
