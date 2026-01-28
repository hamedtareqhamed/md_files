
# UniTask Environment Setup & Deployment Guide (Flutter)

This guide provides a step-by-step walkthrough to set up the **Flutter** development environment for the [UniTask](https://github.com/hamedtareqhamed/UniTask) repository from scratch, covering Windows, Linux, and macOS, and building for Web and Android.

---

## 1. Prerequisites (All Platforms)

* **Git:** For version control.
* **Flutter SDK:** The core framework.
* **Java Development Kit (JDK 17+):** Required for Android gradle builds.
* **Android Studio:** To manage Android SDKs and Emulators.

---

## 2. Platform-Specific Setup

### Windows
1. Download the [Flutter Windows ZIP](https://storage.googleapis.com/flutter_infra_release/releases/stable/windows/flutter_windows_3.38.8-stable.zip) or [backup link](https://docs.flutter.dev/install/manual).
2. Extract to `C:\src\flutter` and add the `bin` folder to your **System PATH**.
3. Run the following command to ensure everything is configured correctly:
```bash
flutter doctor
```
### Linux (Ubuntu)
Install dependencies and Flutter via snap:
```bash
sudo apt update
sudo apt install git curl cmake ninja-build pkg-config libgtk-3-dev liblzma-dev -y
sudo snap install flutter --classic
```
Run the following command to ensure everything is configured correctly:
```bash
flutter doctor
```
### macOS
1. Install Flutter from Homebrew:
```bash
brew install --cask flutter
```
2. Install Xcode for iOS/macOS support:
```bash
xcode-select --install
```
3. Run the following command to ensure everything is configured correctly:
```bash
flutter doctor
```
---

## 3. Project Initialization

Clone the repository and fetch the required packages:
```bash
git clone https://github.com/hamedtareqhamed/UniTask.git
cd UniTask
flutter pub get
```

---

## 4. Compilation & Running

### Web Deployment
To run UniTask in a web browser:
1. **Enable Web support:**
```bash
flutter config --enable-web
```
2. **Run on Chrome:**
```bash
flutter run -d chrome
```
3. **Build for Release:**
```bash
flutter build web
```

---

## 5. Android Deployment

### SDK Configuration
1. Accept the Android licenses:
```bash
flutter doctor --android-licenses
```
2. Connect your device or start an emulator.

### Running & Building
1. **Run on Android:**
```bash
flutter run
```
2. **Build APK (Release):**
```bash
flutter build apk --release
```
3. **Build App Bundle (for Play Store):**
```bash
flutter build appbundle
```

---

