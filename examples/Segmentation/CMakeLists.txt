project(ITKBenchmarkSegmentation)

find_package(ITK REQUIRED
  COMPONENTS
    PerformanceBenchmarking
    ITKIOImageBase
    ITKIOMeta
    ITKCurvatureFlow
    ITKRegionGrowing
    ITKWatersheds
    ITKConnectedComponents
    ITKAnisotropicSmoothing
    ITKFastMarching
    ITKLevelSets
  )
include(${ITK_USE_FILE})

add_executable(RegionGrowingBenchmark RegionGrowingBenchmark.cxx)
target_link_libraries(RegionGrowingBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME RegionGrowingBenchmark
  COMMAND RegionGrowingBenchmark
    ${TEST_OUTPUT_DIR}/RegionGrowingBenchmark.tsv
    3
    -1
    ${BRAIN_IMAGE}
    ${TEST_OUTPUT_DIR}/RegionGrowingBenchmark.mha
  )
set_property(TEST RegionGrowingBenchmark APPEND PROPERTY LABELS Segmentation)

add_executable(WatershedBenchmark WatershedBenchmark.cxx)
target_link_libraries(WatershedBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME WatershedBenchmark
  COMMAND WatershedBenchmark
    ${TEST_OUTPUT_DIR}/WatershedBenchmark.tsv
    3
    -1
    DATA{../Data/Input/brainweb165a10f17extract45i90z.mha}
    ${TEST_OUTPUT_DIR}/WatershedBenchmark.mha
  )
set_property(TEST WatershedBenchmark APPEND PROPERTY LABELS Segmentation)

add_executable(LevelSetBenchmark LevelSetBenchmark.cxx)
target_link_libraries(LevelSetBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME LevelSetBenchmark
  COMMAND LevelSetBenchmark
    ${TEST_OUTPUT_DIR}/LevelSetBenchmark.tsv
    3
    -1
    DATA{../Data/Input/brainweb165a10f17extract60i50z.mha}
    ${TEST_OUTPUT_DIR}/LevelSetBenchmark.mha
  )
set_property(TEST LevelSetBenchmark APPEND PROPERTY LABELS Segmentation)
