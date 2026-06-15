# AirOS Gemini Bridge - Setup & Deployment Guide

## 🚀 Full Automation Setup

### Prerequisites
- Git installed and configured
- Android SDK 33+
- Java 11+ installed
- GitHub account with repository access

---

## 📋 Step 1: Initial Setup

### Clone Repository
```bash
git clone https://github.com/352fihi-beep/AirOS-Gemini-Bridge.git
cd AirOS-Gemini-Bridge
git checkout develop
```

### Set Up Environment
```bash
# Copy example local properties
cp local.properties.example local.properties

# Add your Gemini API key
echo "GEMINI_API_KEY=your_key_here" >> local.properties
```

---

## 🔨 Step 2: Build Options

### Option A: Automated GitHub Actions (Recommended)

**Trigger via GitHub UI:**
1. Go to **Actions** tab
2. Select **Auto Deploy APK - Full Automation**
3. Click **Run workflow**
4. Choose build type (debug/release)
5. Click **Run workflow**

**Trigger via CLI:**
```bash
# Push to develop - automatic build
git push origin develop

# Manual trigger with workflow_dispatch
gh workflow run auto-build-deploy.yml -f build_type=debug
```

### Option B: Local Build Script

```bash
# Make script executable
chmod +x build.sh

# Build debug APK
./build.sh debug

# Build release APK
./build.sh release 1.0.0-prod
```

### Option C: Direct Gradle Commands

```bash
# Debug build
./gradlew assembleDebug

# Release build
./gradlew assembleRelease

# Run tests
./gradlew test

# Run lint
./gradlew lint

# Clean build
./gradlew clean build
```

---

## 🧪 Step 3: Testing

### Run All Tests
```bash
./gradlew test
```

### Run Specific Test
```bash
./gradlew test --tests com.airos.geminibridge.MainActivityTest
```

### Run Instrumented Tests
```bash
./gradlew connectedAndroidTest
```

### View Test Reports
```bash
# After running tests, open:
open app/build/reports/tests/debug/index.html
```

---

## 📦 Step 4: APK Deployment

### GitHub Releases (Automatic)
1. Merge `develop` → `main`
2. Workflow automatically:
   - Builds APK
   - Runs all tests
   - Creates GitHub Release
   - Uploads APK

### Manual Release
```bash
# Create and push tag
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# Workflow triggers automatically
```

### Firebase App Distribution (Optional)

1. **Set up Firebase credentials:**
   ```bash
   # Get Firebase token
   firebase login:ci
   ```

2. **Add GitHub Secrets:**
   - Go to **Settings** → **Secrets and variables** → **Actions**
   - Add `FIREBASE_TOKEN`
   - Add `FIREBASE_APP_ID`

3. **Uncomment Firebase step in workflow** (`.github/workflows/auto-build-deploy.yml`)

4. **Deploy:**
   ```bash
   firebase appdistribution:distribute app-debug.apk \
     --app=YOUR_APP_ID \
     --groups=testers \
     --release-notes="New release"
   ```

---

## 📊 Step 5: Monitor Builds

### View Workflow Status
```bash
# List recent workflows
gh run list --repo 352fihi-beep/AirOS-Gemini-Bridge

# View specific workflow
gh run view <RUN_ID>

# Watch workflow
gh run watch <RUN_ID>
```

### Access Build Artifacts
1. Go to **Actions** tab
2. Select completed workflow
3. Scroll to **Artifacts** section
4. Download:
   - `airos-gemini-bridge-apk` - Built APK
   - `test-reports` - Test results
   - `lint-reports` - Code quality issues

---

## 🔑 GitHub Secrets Configuration

### Required Secrets
```
None required for basic functionality
```

### Optional Secrets (for Firebase deployment)
```
FIREBASE_TOKEN         - Firebase CI token
FIREBASE_APP_ID        - Firebase App ID
```

### Add Secrets via CLI
```bash
gh secret set FIREBASE_TOKEN -b "your_token"
gh secret set FIREBASE_APP_ID -b "your_app_id"
```

---

## 🐛 Troubleshooting

### Build Fails
```bash
# Clean and rebuild
./gradlew clean build --stacktrace

# Check Java version
java -version

# Update SDK
sdkmanager --update
```

### Workflow Permission Issues
1. Go to **Settings** → **Actions** → **General**
2. Set **Workflow permissions** to "Read and write permissions"
3. Enable **"Allow GitHub Actions to create and approve pull requests"**

### Test Failures
```bash
# Run with verbose output
./gradlew test --stacktrace -i

# Check logs
cat app/build/reports/tests/debug/index.html
```

### APK Not Found
```bash
# Verify build directory
ls -la app/build/outputs/apk/

# Check for build errors
./gradlew clean assembleDebug -x lint
```

---

## 📱 Install APK on Device

### Via ADB
```bash
# Connect device via USB
adb devices

# Install APK
adb install app/build/outputs/apk/debug/app-debug.apk

# Run app
adb shell am start -n com.airos.geminibridge/.MainActivity
```

### Via File Manager
1. Download APK from GitHub Releases
2. Transfer to Android device
3. Open file manager and tap APK
4. Allow installation from unknown sources
5. Install

---

## 🔄 Continuous Integration Workflow

### Development Cycle
```
1. Create feature branch
   git checkout -b feature/my-feature develop

2. Make changes and commit
   git add .
   git commit -m "Add feature"

3. Push to GitHub
   git push origin feature/my-feature

4. Create Pull Request
   - Automatic build and tests run
   - Review results in PR

5. Merge to develop
   - Automatic build triggered
   - APK artifacts available

6. Merge to main for release
   - Full build and deployment
   - GitHub Release created
   - APK uploaded
```

---

## 📞 Support

For issues or questions:
1. Check [GitHub Issues](https://github.com/352fihi-beep/AirOS-Gemini-Bridge/issues)
2. View workflow logs in Actions tab
3. Check build reports in artifacts

---

## ✅ Checklist

- [ ] Repository cloned
- [ ] Local.properties configured
- [ ] First build successful
- [ ] Tests passing
- [ ] Workflow triggers on push
- [ ] GitHub Releases working
- [ ] Firebase setup (optional)
- [ ] Team notified of setup

Done! Your Android project is ready for full CI/CD automation. 🎉
