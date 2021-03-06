StandardBRAINSBuildMacro(NAME SmoothingMeshScalars TARGET_LIBRARIES BRAINSCommonLib ${VTK_LIBRARIES}
  ${BRAINSSurfaceTools_ITK_LIBRARIES})

if (BUILD_TESTING AND NOT BRAINSTools_DISABLE_TESTING)

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME TEST_SurfaceSmoothingMeshScalars
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:SmoothingMeshScalars>
          --inputSurfaceFile DATA{${TestData_DIR}/Piecewised_IC4.vtk}
          --outputSurfaceFile SmoothedScalarTest.vtk )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME COMPARE_SurfaceSmoothingMeshScalars
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:CompareSurfaces>
          --inputSurfaceFile SmoothedScalarTest.vtk
          --refSurfaceFile DATA{${TestData_DIR}/SmoothedScalar_IC4.vtk}
          --vertexLocation
          --scalarArray
          --tolerance 1.0e-7 )

set_tests_properties( COMPARE_SurfaceSmoothingMeshScalars PROPERTIES DEPENDS TEST_SurfaceSmoothingMeshScalars )

endif ()
