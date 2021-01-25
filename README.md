# handapp-mediapipe

## Building

This project is packaged with Bazel and uses Mediapipe. Building the main app requires that you have the appropriate system dependencies for building Mediapipe as [specified in its documentation](https://google.github.io/mediapipe/getting_started/install.html).

You should also have an Android SDK and NDK available locally. You can specify
the path to these using the `ANDROID_HOME` and `ANDROID_NDK_HOME` environment
variables. 

Once the dependencies have been installed you can build using:

```shell
$ ANDROID_NDK_HOME=$HOME/path/to/ndk \
  ANDROID_HOME=$HOME/path/to/sdk  \
    bazel build --define MEDIAPIPE_DISABLE_GPU=1 //app/src/main/...
```
