project(ITKBenchmarkRegistration)

find_package(ITK REQUIRED
  COMPONENTS
    PerformanceBenchmarking
    ITKIOImageBase
    ITKIOMeta
    ITKIONRRD
    ITKIOTransformBase
    ITKIOTransformHDF5
    ITKRegistrationMethodsv4
    ITKMetricsv4
    ITKPDEDeformableRegistration
    ITKConvolution
  )
include(${ITK_USE_FILE})

add_executable(RegistrationFrameworkBenchmark RegistrationFrameworkBenchmark.cxx)
target_link_libraries(RegistrationFrameworkBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME RegistrationFrameworkBenchmark
  COMMAND RegistrationFrameworkBenchmark
    ${TEST_OUTPUT_DIR}/RegistrationFrameworkBenchmark.tsv
    3
    -1
    ${BRAIN_IMAGE}
    DATA{../Data/Input/brainweb165a10f17translated-7x-8y9z.nrrd}
    ${TEST_OUTPUT_DIR}/RegistrationFrameworkBenchmark.hdf5
  )
set_property(TEST RegistrationFrameworkBenchmark APPEND PROPERTY LABELS Registration)

add_executable(DemonsRegistrationBenchmark DemonsRegistrationBenchmark.cxx)
target_link_libraries(DemonsRegistrationBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME DemonsRegistrationBenchmark
  COMMAND DemonsRegistrationBenchmark
    ${TEST_OUTPUT_DIR}/DemonsRegistrationBenchmark.tsv
    3
    -1
    ${BRAIN_IMAGE}
    DATA{../Data/Input/brainweb165a10f17translated-1x-1y1z.nrrd}
    ${TEST_OUTPUT_DIR}/DemonsRegistrationBenchmark.mha
  )
set_property(TEST DemonsRegistrationBenchmark APPEND PROPERTY LABELS Registration)

add_executable(NormalizedCorrelationBenchmark NormalizedCorrelationBenchmark.cxx)
target_link_libraries(NormalizedCorrelationBenchmark ${ITK_LIBRARIES})
ExternalData_Add_Test(ITKBenchmarksData
  NAME NormalizedCorrelationBenchmark
  COMMAND NormalizedCorrelationBenchmark
    ${TEST_OUTPUT_DIR}/NormalizedCorrelationBenchmark.tsv
    3
    -1
    DATA{../Data/Input/brainweb165a10f17extract88i5z.mha}
    DATA{../Data/Input/brainweb165a10f17translated-1x-1y1zextract88i5z.mha}
  )
set_property(TEST NormalizedCorrelationBenchmark APPEND PROPERTY LABELS Registration)
