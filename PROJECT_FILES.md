# AirOS Gemini Bridge - Complete Project Files

This document contains all the project files you need to set up your Android development environment.

## File Structure

```
AirOS-Gemini-Bridge/
├── .github/
│   └── workflows/
│       └── build-and-deploy.yml
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/airos/geminibridge/
│   │   │   │   └── MainActivity.kt
│   │   │   ├── res/
│   │   │   │   └── layout/
│   │   │   │       └── activity_main.xml
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   │       └── java/com/airos/geminibridge/
│   │           └── MainActivityTest.kt
│   └── build.gradle
├── .gitignore
├── build.gradle
├── settings.gradle
└── README.md
```

## Installation Steps

1. Clone or create the directory structure as shown above
2. Copy each file from the sections below into the corresponding location
3. Run `./gradlew build` to build the project
4. The GitHub Actions workflow will automatically trigger on push

---

## FILES CONTENT

### 1. .github/workflows/build-and-deploy.yml
[CI/CD Workflow File - see below]

### 2. build.gradle
[Root Build Configuration - see below]

### 3. app/build.gradle
[App Build Configuration - see below]

### 4. settings.gradle
[Settings Configuration - see below]

### 5. app/src/main/AndroidManifest.xml
[Android Manifest - see below]

### 6. app/src/main/java/com/airos/geminibridge/MainActivity.kt
[Main Activity - see below]

### 7. app/src/main/res/layout/activity_main.xml
[Activity Layout - see below]

### 8. app/src/test/java/com/airos/geminibridge/MainActivityTest.kt
[Unit Tests - see below]

### 9. .gitignore
[Git Ignore Configuration - see below]

### 10. README.md
[Project Documentation - see below]

---

## Quick Setup

```bash
# 1. Create project structure
mkdir -p AirOS-Gemini-Bridge/{.github/workflows,app/src/main/java/com/airos/geminibridge,app/src/main/res/layout,app/src/test/java/com/airos/geminibridge}

# 2. Navigate to project
cd AirOS-Gemini-Bridge

# 3. Copy all files from this package

# 4. Build the project
./gradlew build

# 5. Run tests
./gradlew test

# 6. Build APK
./gradlew assembleDebug
```

See individual file sections below for complete content.
