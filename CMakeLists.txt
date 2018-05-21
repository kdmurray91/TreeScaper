PROJECT(TreeScaper)
CMAKE_MINIMUM_REQUIRED(VERSION 3.0)

LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake-modules")

# Cmake options
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

IF (NOT CMAKE_BUILD_TYPE)
        SET(CMAKE_BUILD_TYPE Release)
ENDIF()

#set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
#set(BLA_STATIC ON)
#set(BLA_VENDOR OpenBLAS)

###############################
## Find Packages and Headers ##
###############################

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5 COMPONENTS Core Widgets Gui PrintSupport WebKitWidgets REQUIRED)
find_package(VTK REQUIRED)
include(${VTK_USE_FILE})
find_package(LAPACK REQUIRED)
add_compile_options(-DTS_CMAKE_LAPACK=1)


set(TS_SRCS main.cpp randgen.cpp treescaper.cpp wstring.cpp warray.cpp wfile.cpp wDimEst.cpp wmatrix.cpp
    wNLDR.cpp wImage.cpp setting.cpp wNLDRthread.cpp wPlotthread.cpp wPlotTreethread.cpp wPlotTree.cpp
    wDimestthread.cpp wPlotdimthread.cpp hash.cc hashfunc.cc label-map.cc hungarian.c Sparse_matrix.cpp
    PointsSource.cpp community.cpp graph.cpp greedy_louvain.cpp info.cpp MersenneTwister.cpp slicer.cpp
    PlotGraph.cpp Trees.cpp TreeOPE.cpp plot2d.cpp qcustomplot.cpp wCommunitythread.cpp woutput.cpp
    ClusterForest.cpp ClusterInstance.cpp Forest.cpp rspr.cpp SiblingPair.cpp SPRLCA.cpp SPRNode.cpp
    UndoMachine.cpp NLDRsetting.cpp)

add_executable(TreeScaper ${TS_SRCS})
target_link_libraries(TreeScaper Qt5::Widgets Qt5::Core Qt5::Gui Qt5::WebKitWidgets Qt5::PrintSupport ${VTK_LIBRARIES} ${BLAS_LIBRARIES} ${LAPACK_LIBRARIES})

