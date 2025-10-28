# React Native Social Media App - Complete Setup Guide

## 📱 Complete TypeScript/TSX Implementation

This is a full-featured social media mobile app built with:
- **React Native** with TypeScript
- **React Navigation** for routing
- **Socket.IO** for real-time chat
- **Axios** for API calls
- **AsyncStorage** for local data
- **React Native Image Picker** for media

---

## 🚀 Quick Start

### Prerequisites Installed:
- Node.js (v18+)
- JDK 11 or 17
- Android SDK
- VS Code

### 1. Install Dependencies

```bash
cd mobile-app
npm install
```

### 2. Setup Android

**For Windows:**
```bash
cd android
gradlew.bat clean
cd ..
```

**For Mac/Linux:**
```bash
cd android
./gradlew clean
cd ..
```

### 3. Update Environment Variables

Edit `.env` file:
```env
# For Android Emulator
API_URL=http://10.0.2.2:5000
SOCKET_URL=http://10.0.2.2:5000

# For Physical Device (replace with your computer's IP)
# API_URL=http://192.168.1.XXX:5000
# SOCKET_URL=http://192.168.1.XXX:5000
```

To find your computer's IP:
- **Windows:** `ipconfig` in CMD
- **Mac/Linux:** `ifconfig` or `ip addr`

### 4. Add Default Avatar Image

Add a default avatar image to `assets/default-avatar.png`

**Quick solution - Create programmatically:**
```bash
# Download a placeholder
curl -o assets/default-avatar.png https://ui-avatars.com/api/?name=User&size=500&background=007AFF&color=fff
```

Or place any 500x500px avatar image as `assets/default-avatar.png`

### 5. Update Android Permissions

The following permissions are already configured in `android/app/src/main/AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" android:maxSdkVersion="32" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="32" />
```

And add to `<application>` tag:
```xml
android:usesCleartextTraffic="true"
```

### 6. Start the App

**Terminal 1 - Start Metro Bundler:**
```bash
npm start
```

**Terminal 2 - Run on Android:**
```bash
npm run android
```

---

## 📁 Project Structure

```
mobile-app/
├── src/
│   ├── api/
│   │   └── api.ts                 # Axios configuration
│   │
│   ├── components/
│   │   ├── Button.tsx            # Reusable button component
│   │   ├── PostCard.tsx          # Post display component
│   │   ├── Loading.tsx           # Loading screen
│   │   └── index.ts              # Component exports
│   │
│   ├── navigation/
│   │   └── AppNavigator.tsx      # Navigation setup
│   │
│   ├── screens/
│   │   ├── LoginScreen.tsx       # Login page
│   │   ├── SignupScreen.tsx      # Signup page
│   │   ├── HomeScreen.tsx        # Feed/timeline
│   │   ├── CreatePostScreen.tsx  # Create new post
│   │   ├── ProfileScreen.tsx     # User profile
│   │   ├── EditProfileScreen.tsx # Edit profile
│   │   ├── ChatScreen.tsx        # Real-time chat
│   │   └── index.ts              # Screen exports
│   │
│   ├── types/
│   │   └── index.ts              # TypeScript interfaces
│   │
│   ├── utils/
│   │   └── storage.ts            # AsyncStorage helpers
│   │
│   └── env.d.ts                  # Environment types
│
├── assets/
│   ├── default-avatar.png        # Default profile picture
│   └── README.md
│
├── android/                       # Android build files
├── App.tsx                        # Root component
├── package.json
├── tsconfig.json                  # TypeScript config
├── babel.config.js               # Babel config
└── .env                          # Environment variables
```

---

## 🔧 Configuration Files

### TypeScript Configuration (`tsconfig.json`)
- Strict type checking enabled
- Path aliases configured
- React Native specific settings

### Babel Configuration (`babel.config.js`)
- React Native preset
- Environment variables plugin
- Reanimated plugin

### Environment Variables (`.env`)
- API_URL: Backend server URL
- SOCKET_URL: WebSocket server URL

---

## 📱 Features Implementation

### ✅ Authentication
- Login with email/password
- Signup with validation
- Token-based authentication
- Auto-login on app start

### ✅ Posts
- Create posts with text and images
- Like/unlike posts
- Comment on posts
- View all posts feed
- Pull to refresh

### ✅ Profile
- View user profiles
- Edit profile (username, bio, photo)
- Logout functionality

### ✅ Real-time Chat
- One-on-one messaging
- Socket.IO integration
- Real-time message updates
- Message history

### ✅ Image Upload
- Profile picture upload
- Post image upload
- Image picker integration
- Image compression

---

## 🐛 Common Issues & Solutions

### Issue 1: "Cannot find module '@env'"
**Solution:**
```bash
npm start -- --reset-cache
```

### Issue 2: "Default avatar not found"
**Solution:**
Add any placeholder image as `assets/default-avatar.png` or download:
```bash
curl -o assets/default-avatar.png https://ui-avatars.com/api/?name=User&size=500
```

### Issue 3: "Unable to connect to server"
**Solution:**
- For Emulator: Use `http://10.0.2.2:5000`
- For Device: Use your computer's local IP
- Check backend server is running
- Update `.env` file

### Issue 4: Build fails
**Solution:**
```bash
cd android
./gradlew clean
cd ..
npx react-native start --reset-cache
```

### Issue 5: "Cleartext HTTP traffic not permitted"
**Solution:**
Add to `AndroidManifest.xml` in `<application>` tag:
```xml
android:usesCleartextTraffic="true"
```

### Issue 6: Image picker not working
**Solution:**
Add permissions to `AndroidManifest.xml` and request runtime permissions on Android 13+

### Issue 7: Socket connection failed
**Solution:**
- Check SOCKET_URL in `.env`
- Ensure backend Socket.IO server is running
- Check firewall settings

---

## 🧪 Testing the App

### 1. Test Authentication
- Create a new account
- Logout
- Login with credentials
- Check token persistence

### 2. Test Posts
- Create a text post
- Create a post with image
- Like a post
- Comment on a post
- Pull to refresh

### 3. Test Profile
- View your profile
- Edit profile info
- Change profile picture
- View another user's profile

### 4. Test Chat
- Open chat with a user
- Send messages
- Receive real-time messages
- Check message history

---

## 📦 Building APK

### Debug APK (for testing)
```bash
cd android
./gradlew assembleDebug
```
Location: `android/app/build/outputs/apk/debug/app-debug.apk`

### Release APK (for distribution)

1. **Generate signing key:**
```bash
cd android/app
keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

2. **Configure gradle.properties:**
```properties
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=your_password
MYAPP_RELEASE_KEY_PASSWORD=your_password
```

3. **Update build.gradle:**
Add in `android/app/build.gradle`:
```gradle
signingConfigs {
    release {
        if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
}
buildTypes {
    release {
        signingConfig signingConfigs.release
        minifyEnabled true
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
}
```

4. **Build:**
```bash
cd android
./gradlew assembleRelease
```

Location: `android/app/build/outputs/apk/release/app-release.apk`

---

## 🔍 Code Quality

### Type Safety
- Full TypeScript coverage
- Strict type checking
- Proper interface definitions
- No `any` types except for necessary cases

### Error Handling
- Try-catch blocks for async operations
- User-friendly error messages
- Graceful fallbacks

### Performance
- Optimized re-renders
- Proper key usage in lists
- Image optimization
- Lazy loading where applicable

---

## 📚 Key Dependencies

```json
{
  "@react-navigation/native": "Navigation framework",
  "@react-navigation/stack": "Stack navigator",
  "@react-navigation/bottom-tabs": "Tab navigator",
  "react-native-gesture-handler": "Gesture handling",
  "react-native-reanimated": "Animations",
  "axios": "HTTP client",
  "socket.io-client": "Real-time communication",
  "@react-native-async-storage/async-storage": "Local storage",
  "react-native-image-picker": "Image selection",
  "react-native-dotenv": "Environment variables"
}
```

---

## 🚀 Next Steps

1. **Add more features:**
   - Search users
   - Follow/unfollow
   - Notifications
   - Stories
   - Video posts

2. **Improve UI/UX:**
   - Better animations
   - Dark mode
   - Custom themes
   - Skeleton loaders

3. **Add testing:**
   - Unit tests with Jest
   - Integration tests
   - E2E tests with Detox

4. **Optimize:**
   - Code splitting
   - Image caching
   - Performance monitoring
   - Analytics

---

## 💡 Tips

- Always clean build when dependencies change
- Use TypeScript strict mode
- Handle loading and error states
- Test on both emulator and real device
- Keep dependencies updated
- Use proper navigation patterns
- Implement proper authentication flow

---

## 🆘 Getting Help

If you encounter issues:

1. Check error messages in terminal
2. Review React Native logs: `npx react-native log-android`
3. Clean build: `cd android && ./gradlew clean`
4. Reset cache: `npm start -- --reset-cache`
5. Check backend is running
6. Verify environment variables

---

**Built with ❤️ using React Native + TypeScript**

Happy Coding! 🚀