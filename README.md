# Android Emulator Cloud

Run Android emulators in Docker containers with noVNC support and cloud-native deployment capabilities.

## Overview

This project provides a Docker-based solution for running Android emulators in the cloud. It supports multiple Android versions, device profiles, and can be deployed on various cloud platforms including AWS, Azure, GCP, and Alibaba Cloud.

## Features

- **Multi-version Android Emulators**: Support for Android 9.0 through Android 14.0
- **Multiple Device Profiles**: Samsung Galaxy S10/S9/S8, Nexus 4/5/One/S, Pixel C, and more
- **noVNC Support**: Access the emulator through any web browser via VNC protocol
- **ADB Connectivity**: Control the emulator from outside the container
- **Cloud-Native**: Designed for deployment on cloud infrastructure
- **CI/CD Integration**: Works seamlessly with Jenkins, GitHub Actions, and other CI systems
- **Video Recording**: Record emulator sessions for debugging and testing
- **Flexible Storage**: Persist emulator data across container restarts via volume mounts

## Supported Android Versions

| Android | API | Tag |
|---------|-----|-----|
| 9.0 | 28 | emulator_9.0 |
| 10.0 | 29 | emulator_10.0 |
| 11.0 | 30 | emulator_11.0 |
| 12.0 | 32 | emulator_12.0 |
| 13.0 | 33 | emulator_13.0 |
| 14.0 | 34 | emulator_14.0 |

## Quick Start

### Prerequisites

1. Docker installed on your system
2. KVM virtualization enabled (Linux) or WSL2 with virtualization (Windows 11)

### Run Your First Android Emulator

`ash
# Run an Android 11 emulator with noVNC access
docker run -d \
  -p 6080:6080 \
  -e EMULATOR_DEVICE="Samsung Galaxy S10" \
  -e WEB_VNC=true \
  --device /dev/kvm \
  --name android-emulator \
  budtmo/docker-android:emulator_11.0
`

Then open **http://localhost:6080** in your browser to access the emulator.

### Persist Data

`ash
docker run -d \
  -v data:/home/androidusr \
  -p 6080:6080 \
  -e EMULATOR_DEVICE="Samsung Galaxy S10" \
  --device /dev/kvm \
  --name android-emulator \
  budtmo/docker-android:emulator_11.0
`

## Cloud Deployment

This project supports deployment on major cloud platforms:

- **AWS**: ECS, EKS, or EC2 with KVM
- **Azure**: Azure Container Instances with nested virtualization
- **GCP**: Compute Engine with KVM support
- **Alibaba Cloud**: ECS with GPU or KVM instances

## Use Cases

- Mobile app automated testing (Appium, Espresso)
- CI/CD pipeline integration for Android projects
- Cloud-based device testing labs
- Accessibility and UI testing
- SMS simulation for testing
- Android build automation

## Architecture

The Docker image includes:
- Base Ubuntu 20.04
- Android SDK with command-line tools
- Android emulator binaries
- noVNC for web-based access
- OpenSSH for ADB connectivity
- Web-based log viewer

## License

MIT License

---

Made with 鉂わ笍 for cloud phone automation 鈫?[qtphone.com](https://www.qtphone.com/)