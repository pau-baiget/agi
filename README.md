# Android GPU Inspector

<!-- TODO(b/155159330) Once we reach a stable release, re-enabled godoc and switch to pkg.go.dev, see https://go.dev/about#adding-a-package -->
<!-- [![GoDoc](https://godoc.org/github.com/google/gapid?status.svg)](https://godoc.org/github.com/google/gapid) -->
![](./kokoro/img/linux.png)
<img alt="Linux" src="kokoro/img/linux.png" width="20px" height="20px" hspace="2px"/>
[![Linux Build Status](https://agi-build.storage.googleapis.com/badges/build_status_linux.svg)](https://agi-build.storage.googleapis.com/badges/build_result_linux.html)
<img alt="MacOS" src="kokoro/img/macos.png" width="20px" height="20px" hspace="2px"/>
[![MacOS Build Status](https://agi-build.storage.googleapis.com/badges/build_status_macos.svg)](https://agi-build.storage.googleapis.com/badges/build_result_macos.html)
<img alt="Windows" src="kokoro/img/windows.png" width="20px" height="20px" hspace="2px"/>
[![Windows Build Status](https://agi-build.storage.googleapis.com/badges/build_status_windows.svg)](https://agi-build.storage.googleapis.com/badges/build_result_windows.html)

## Downloads

**[Download the latest version of AGI here.](https://github.com/google/agi/releases)**

*Unstable* developer releases are [here](https://github.com/google/agi-dev-releases/releases).

## Documentation

**[User documentation can be found at gpuinspector.dev](https://gpuinspector.dev)**

The [developer documentation](DEVDOC.md) contains some hints for AGI
developers. See also the README files under some source directories.

## About

Android GPU Inspector is a collection of tools that allows you to inspect, tweak and replay calls from an application to a graphics driver.

Android GPU Inspector can trace any Android [debuggable application](https://developer.android.com/guide/topics/manifest/application-element.html#debug), or if you have root access to the device any application can be traced.
AGI can also trace any desktop Vulkan application.

<table>
  <tr>
    <td>
      <a href="https://gpuinspector.dev/images/screenshots/framebuffer.png">
        <img src="https://gpuinspector.dev/images/screenshots/framebuffer_thumb.jpg" alt="Screenshot 1">
      </a>
    </td>
    <td>
      <a href="https://gpuinspector.dev/images/screenshots/geometry.png">
        <img src="https://gpuinspector.dev/images/screenshots/geometry_thumb.jpg" alt="Screenshot 2">
      </a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://gpuinspector.dev/images/screenshots/textures.png">
        <img src="https://gpuinspector.dev/images/screenshots/textures_thumb.jpg" alt="Screenshot 3">
      </a>
    </td>
    <td>
      <a href="https://gpuinspector.dev/images/screenshots/shaders.png">
        <img src="https://gpuinspector.dev/images/screenshots/shaders_thumb.jpg" alt="Screenshot 4">
      </a>
    </td>
  </tr>
</table>

## Building

**See [Building Android GPU Inspector](BUILDING.md).**

## Running the client

After building AGI, you can run the client from `<agi-root>/bazel-bin/pkg/gapid`.

## Command-Line Interface

AGI exposes most of its functionality via a CLI *gapit*. You can find auto-generated documentation [here](https://gpuinspector.dev/cli/).

## Project Structure

Android GPU Inspector consists of the following sub-components:

### [`gapii`](gapii): Graphics API Interceptor
A layer that sits between the application / game and the GPU driver, recording all the calls and memory accesses.

### [`gapis`](gapis): Graphics API Server
A process that analyses capture streams reporting incorrect API usage, processes the data for replay on various target devices, and provides an RPC interface to the client.

### [`gapir`](gapir): Graphics API Replay daemon
A stack-based VM used to playback capture files, imitating the original application’s / game's calls to the GPU driver. Supports read-back of any buffer / framebuffer, and provides profiling functionality.

### [`gapic`](gapic): Graphics API Client
The frontend user interface application. Provides visual inspection of the capture data, memory, resources, and frame-buffer content.

### [`gapil`](gapil): Graphics API Language
A new domain specific language to describe a graphics API in its entirety. Combined with our template system to generate huge parts of the interceptor, server and replay systems.
