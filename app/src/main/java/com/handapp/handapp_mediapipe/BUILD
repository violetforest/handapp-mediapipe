load("@build_bazel_rules_android//android:rules.bzl", "android_binary")
load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

# Note: Anything prefixed with @mediapipe is a reference to the
# the external google/mediapipe repository

cc_binary(
    name = "libmediapipe_jni.so",
    linkshared = 1,
    linkstatic = 1,
    deps = [
        "@mediapipe//mediapipe/graphs/hand_tracking:mobile_calculators",
        "@mediapipe//mediapipe/java/com/google/mediapipe/framework/jni:mediapipe_framework_jni",
    ],
)

cc_library(
    name = "mediapipe_jni_lib",
    srcs = [":libmediapipe_jni.so"],
    alwayslink = 1,
)


android_binary(
    name = "handtrackinggpu",
    srcs = glob(["*.java"]),
    assets = [
        # TODO: Getting bazel runtime errors resolving this target.
        #"@mediapipe//mediapipe/graphs/hand_tracking:hand_tracking_mobile_gpu.binarypb",
        "@mediapipe//mediapipe/modules/hand_landmark:handedness.txt",
        "@mediapipe//mediapipe/modules/hand_landmark:hand_landmark.tflite",
        "@mediapipe//mediapipe/modules/palm_detection:palm_detection.tflite",
    ],
    assets_dir = "",
    # TODO: Plug in our own manifest file
    manifest = "@mediapipe//mediapipe/examples/android/src/java/com/google/mediapipe/apps/basic:AndroidManifest.xml",
    manifest_values = {
        "applicationId": "com.google.mediapipe.apps.handtrackinggpu",
        "appName": "Hand Tracking",
        "mainActivity": ".MainActivity",
        "cameraFacingFront": "True",
        "binaryGraphName": "hand_tracking_mobile_gpu.binarypb",
        "inputVideoStreamName": "input_video",
        "outputVideoStreamName": "output_video",
        "flipFramesVertically": "True",
        "converterNumBuffers": "2",
    },
    resource_files = glob(["res/**"]),
    multidex = "native",
    # TODO: Check which of these we actually need
    deps = [
        ":mediapipe_jni_lib",
        "@mediapipe//mediapipe/examples/android/src/java/com/google/mediapipe/apps/basic:basic_lib",
        "@mediapipe//mediapipe/framework/formats:landmark_java_proto_lite",
        "@mediapipe//mediapipe/java/com/google/mediapipe/framework:android_framework",
    ],
)
