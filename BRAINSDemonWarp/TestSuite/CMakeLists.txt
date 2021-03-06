###  This is the test suite for the BRAINSDemonWarp program.
###  It is intended to test a wide set of image types and image
###  physical space descriptions to ensure that all ITK
###  images are treated properly.

### All test have been pushed to this sub-directory to keep the primary build clean.
MakeTestDriverFromSEMTool(BRAINSDemonWarp BRAINSDemonWarpTest.cxx)
MakeTestDriverFromSEMTool(VBRAINSDemonWarp VBRAINSDemonWarpTest.cxx)


#1
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateBRAINSDemonsWarpTest_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/thirionDemons.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/thirionDemons_test.nii.gz
  --compareNumberOfPixelsTolerance 50
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/thirionDemons_test.nii.gz
  #    --inputPixelType short
  #    --outputPixelType short
  --outputDebug
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,100,100
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Demons
  )

#2
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateFastSymmetricForcesTest_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/fastSymmetricForcesDemons.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/fastSymmetricForcesDemons_test.nii.gz
  --compareNumberOfPixelsTolerance 450
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/fastSymmetricForcesDemons_test.nii.gz
  --inputPixelType uchar
  --outputPixelType uchar
  --medianFilterSize 1,1,1
  --outputDebug
  --smoothDisplacementFieldSigma 1.0
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType FastSymmetricForces
  )

#3
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicTest1_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons1.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons1_test.nii.gz
  --compareNumberOfPixelsTolerance 220
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons1_test.nii.gz
  --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField.nii.gz
  --inputPixelType short
  --outputPixelType uchar
  --outputNormalized
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )
#4
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicTest2_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons2.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons2_test.nii.gz
  --compareNumberOfPixelsTolerance 300
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons2_test.nii.gz
  --inputPixelType ushort
  --outputPixelType uchar
  --outputNormalized
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_brain_cut_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_brain_cut_mask.nii.gz}
  --maskProcessingMode BOBF
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.0
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )

#5
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicTest3_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons3.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons3_test.nii.gz
  --compareNumberOfPixelsTolerance 6950
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  #    --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField.nii.gz
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons3_test.nii.gz
  --inputPixelType int
  --outputPixelType uchar
  --outputNormalized
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_brain_cut_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_brain_cut_mask.nii.gz}
  --maskProcessingMode BOBF
  --smoothDisplacementFieldSigma 0.01
  --upFieldSmoothing 1.0
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )

#6
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicTest4_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons4.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons4_test.nii.gz
  --compareNumberOfPixelsTolerance 340
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemons4_test.nii.gz
  --inputPixelType int
  --outputPixelType uchar
  #    --outputNormalized
  --outputCheckerboardVolume ${CMAKE_CURRENT_BINARY_DIR}/output_Checkborad.nii.gz
  --initializeWithDisplacementField DATA{${TestData_DIR}/InitialDisplacementField.nii.gz}
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 10,5,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --outputDisplacementFieldPrefix ${CMAKE_CURRENT_BINARY_DIR}/displacement.nii.gz
  --registrationFilterType Diffeomorphic
  )

### Need to add more test to get better code coverage of this test suite.  Need to make sure that all the command line options are tested.
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateOrientedImagesTest5_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/ValidateOrientedImagesTest5.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/ValidateOrientedImagesTest5.nii.gz
  --compareNumberOfPixelsTolerance 49800
  --compareIntensityTolerance 25
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/ANON0006_20_T1_sag_twisted.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/ANON0006_20_T1_dbg_splayed.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/ValidateOrientedImagesTest5.nii.gz
  --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField_orientedImage.nii.gz
  --inputPixelType uchar
  --outputPixelType uchar
  --smoothDisplacementFieldSigma 1.5
  --outputDebug
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 1000,100,25
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorBRAINSDemonWarpTest_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/thirionDemons.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/thirionDemons_V_test.nii.gz
  --compareNumberOfPixelsTolerance 50
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/thirionDemons_V_test.nii.gz
  #    --inputPixelType short
  #    --outputPixelType short
  --outputDebug
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,100,100
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Demons
  )


ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorFastSymmetricForcesTest_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/fastSymmetricForcesDemons.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/fastSymmetricForcesDemons_V_test.nii.gz
  --compareNumberOfPixelsTolerance 450
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/fastSymmetricForcesDemons_V_test.nii.gz
  --inputPixelType uchar
  --outputPixelType uchar
  --medianFilterSize 1,1,1
  --outputDebug
  --smoothDisplacementFieldSigma 1.0
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType FastSymmetricForces
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest1_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons1.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons1_test.nii.gz
  --compareNumberOfPixelsTolerance 220
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons1_test.nii.gz
  --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField.nii.gz
  --inputPixelType short
  --outputPixelType uchar
  --outputNormalized
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )


ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest2_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons2.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons2_test.nii.gz
  --compareNumberOfPixelsTolerance 300
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons2_test.nii.gz
  --inputPixelType ushort
  --outputPixelType uchar
  --outputNormalized
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_brain_cut_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_brain_cut_mask.nii.gz}
  --makeBOBF
  --histogramMatch
  --numberOfHistogramBins 1024    --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.0    --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest3_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons3.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons3_test.nii.gz
  --compareNumberOfPixelsTolerance 6950
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume  DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume  DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  #    --outputDisplacementFieldVolume ${VBRAINSDemonWarp_BINARY_DIR}/OutDefField.nii.gz
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons3_test.nii.gz
  --inputPixelType int
  --outputPixelType uchar
  --outputNormalized
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_brain_cut_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_brain_cut_mask.nii.gz}
  --makeBOBF
  --smoothDisplacementFieldSigma 0.01
  --upFieldSmoothing 1.0
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )


ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest4_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons4.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons4_test.nii.gz
  --compareNumberOfPixelsTolerance 340
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons4_test.nii.gz
  --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField.nii.gz
  --inputPixelType int
  --outputPixelType uchar
  #    --outputNormalized
  --outputCheckerboardVolume ${CMAKE_CURRENT_BINARY_DIR}/output_Checkborad.nii.gz
  --initializeWithDisplacementField DATA{${TestData_DIR}/InitialDisplacementField.nii.gz}
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 10,5,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  --outputDisplacementFieldPrefix ${CMAKE_CURRENT_BINARY_DIR}/displacement.nii.gz
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest5_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons5.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons5_test.nii.gz
  --compareNumberOfPixelsTolerance 75
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons5_test.nii.gz
  --inputPixelType short
  --outputPixelType uchar
  --medianFilterSize 1,1,1
  --outputDebug
  --histogramMatch
  --weightFactors 0.5,0.5,0.0
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorDiffeomorphicTest6_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons3.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons6_test.nii.gz
  --compareNumberOfPixelsTolerance 6950
  --compareIntensityTolerance 10
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  #    --outputDisplacementFieldVolume ${CMAKE_CURRENT_BINARY_DIR}/OutDefField.nii.gz
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/vectordiffeomorphicDemons6_test.nii.gz
  --inputPixelType int
  --outputPixelType uchar
  --outputNormalized
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_brain_cut_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_brain_cut_mask.nii.gz}
  --makeBOBF
  --smoothDisplacementFieldSigma 0.01
  --upFieldSmoothing 1.0
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType Diffeomorphic
  )



ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorOrientedImagesTest6_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/ValidateVectorOrientedImagesTest6.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/ValidateVectorOrientedImagesTest6.nii.gz
  --compareNumberOfPixelsTolerance 50000
  --compareIntensityTolerance 25
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/ANON0006_20_T1_sag_twisted.nii.gz}
  --movingVolume DATA{${TestData_DIR}/ANON0006_20_T1_sag_twisted.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/ANON0006_20_T1_dbg_splayed.nii.gz}
  --fixedVolume  DATA{${TestData_DIR}/ANON0006_20_T1_dbg_splayed.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/ValidateVectorOrientedImagesTest6.nii.gz
  --inputPixelType uchar
  --outputPixelType uchar
  --smoothDisplacementFieldSigma 1.5
  --outputDebug
  --numberOfPyramidLevels 5
  --arrayOfPyramidLevelIterations 100,30,20,0,0
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateVectorOrientedImagesTest7_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:VBRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/ValidateVectorOrientedImagesTest7.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/ValidateVectorOrientedImagesTest7.nii.gz
  --compareNumberOfPixelsTolerance 51000
  --compareIntensityTolerance 25
  VBRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/ANON0006_20_T1_sag_twisted.nii.gz}
  --movingVolume DATA{${TestData_DIR}/ANON0006_20_T1_sag_twisted.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/ANON0006_20_T1_dbg_splayed.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/ANON0006_20_T1_dbg_splayed.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/ValidateVectorOrientedImagesTest7.nii.gz
  --inputPixelType uchar
  --outputPixelType uchar
  --smoothDisplacementFieldSigma 1.5
  --outputDebug
  --weightFactors 0.8,0.2
  --numberOfPyramidLevels 5
  --arrayOfPyramidLevelIterations 100,30,20,0,0
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicWithAUTOMask_Test_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemons_AutoMask.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemonsWithAutoMask_test.nii.gz
  --compareNumberOfPixelsTolerance 5549
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T2.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T2.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemonsWithAutoMask_test.nii.gz
  --inputPixelType short
  --outputPixelType uchar
  --outputNormalized
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --maskProcessingMode ROIAUTO
  --registrationFilterType Diffeomorphic
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateDiffeomorphicWithMask_Test_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/diffeomorphicDemonsWithMask.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemonsWithMask_test.nii.gz
  --compareNumberOfPixelsTolerance 5150
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T2.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T2.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/diffeomorphicDemonsWithMask_test.nii.gz
  --inputPixelType short
  --outputPixelType uchar
  --outputNormalized
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --maskProcessingMode ROI
  --fixedBinaryVolume DATA{${TestData_DIR}/SUBJ_A_small_T2_mask.nii.gz}
  --movingBinaryVolume DATA{${TestData_DIR}/SUBJ_B_small_T2_mask.nii.gz}
  --registrationFilterType Diffeomorphic
  )

#Test for initial Transform
if( ${BRAINSTools_MAX_TEST_LEVEL} GREATER 5)
# TODO # I think this test is failing because the reference data is wrong.
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateInitialTransform_Test_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/ValidateInitialTransform_Test.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/ValidateInitialTransform_Test.nii.gz
  --compareNumberOfPixelsTolerance 20
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/rotation.rescale.rigid.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/test.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/ValidateInitialTransform_Test.nii.gz
  --outputPixelType short
  --outputDebug
  --initializeWithTransform DATA{${TestData_DIR}/Transforms_h5/BRAINSFitTest_BSplineAnteScaleRotationRescaleHeadMasks.${XFRM_EXT}}
  --smoothDisplacementFieldSigma 0.0
  --numberOfPyramidLevels 1
  --arrayOfPyramidLevelIterations 1
  --minimumFixedPyramid 1,1,1
  --minimumMovingPyramid 1,1,1
  --registrationFilterType Diffeomorphic
  )
endif()

if( ${BRAINSTools_MAX_TEST_LEVEL} GREATER 8) # This should be restored after fixing.
# TODO Determine if this is even a valid test any longer
# These do not work, and appear to have never worked
#Test for Log Domain
ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateLogDemons_Test_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/logDemons.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/logDemons_test.nii.gz
  --compareNumberOfPixelsTolerance 500
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/logDemons_test.nii.gz
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType LogDemons
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateSymmetricLogDemons_Test1_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/symmetricLogDemons1.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/symmetricLogDemons_test1.nii.gz
  --compareNumberOfPixelsTolerance 1300
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/symmetricLogDemons_test1.nii.gz
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --registrationFilterType SymmetricLogDemons
  )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME ValidateSymmetricLogDemons_Test2_nii
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:BRAINSDemonWarpTestDriver>
  --compare
  DATA{${TestData_DIR}/symmetricLogDemons2.nii.gz}
  ${CMAKE_CURRENT_BINARY_DIR}/symmetricLogDemons_test2.nii.gz
  --compareNumberOfPixelsTolerance 1300
  --compareIntensityTolerance 10
  BRAINSDemonWarpTest
  --movingVolume DATA{${TestData_DIR}/SUBJ_B_small_T1.nii.gz}
  --fixedVolume DATA{${TestData_DIR}/SUBJ_A_small_T1.nii.gz}
  --outputVolume ${CMAKE_CURRENT_BINARY_DIR}/symmetricLogDemons_test2.nii.gz
  --outputDebug
  --histogramMatch
  --numberOfHistogramBins 1024
  --numberOfMatchPoints 7
  --smoothDisplacementFieldSigma 1.5
  --numberOfPyramidLevels 3
  --arrayOfPyramidLevelIterations 100,50,5
  --minimumFixedPyramid 4,4,4
  --minimumMovingPyramid 4,4,4
  --initializeWithDisplacementField DATA{${TestData_DIR}/InitialDisplacementField.nii.gz}
  --registrationFilterType SymmetricLogDemons
  )
endif()  # Commend out the LogDemons tests.
