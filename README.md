# Social Media App - Simple & Easy

A simple social media app for Android built with React Native and Node.js backend. Post updates, like, comment, and chat with friends!

## 📱 Features

- Login & Signup
- Create posts with images
- Like and comment on posts
- View user profiles
- Real-time chat
- Edit your profile

## 🛠️ Tech Stack

**Backend:** Node.js + Express + MongoDB + Socket.io  
**Frontend:** React Native (Android only)

## 📁 Simple Project Structure

```
social-media-app/
│
├── backend/                    # Server code
│   ├── models/
│   │   ├── User.js            # User database model
│   │   ├── Post.js            # Post database model
│   │   └── Message.js         # Chat message model
│   │
│   ├── routes/
│   │   ├── auth.js            # Login/Signup routes
│   │   ├── posts.js           # Post routes
│   │   ├── users.js           # User profile routes
│   │   └── chat.js            # Chat routes
│   │
│   ├── middleware/
│   │   └── auth.js            # Check if user is logged in
│   │
│   ├── uploads/               # Uploaded images folder
│   ├── server.js              # Main server file
│   ├── .env                   # Secret keys
│   └── package.json
│
└── mobile/                     # React Native App
    ├── src/
    │   ├── screens/           # All app screens
    │   │   ├── LoginScreen.js
    │   │   ├── SignupScreen.js
    │   │   ├── HomeScreen.js
    │   │   ├── CreatePostScreen.js
    │   │   ├── ProfileScreen.js
    │   │   └── ChatScreen.js
    │   │
    │   ├── components/        # Reusable UI pieces
    │   │   ├── PostCard.js
    │   │   ├── Comment.js
    │   │   └── Button.js
    │   │
    │   ├── api/              # Talk to server
    │   │   └── api.js
    │   │
    │   ├── navigation/       # Screen navigation
    │   │   └── AppNavigator.js
    │   │
    │   └── utils/           # Helper functions
    │       └── storage.js   # Save user data
    │
    ├── android/             # Android build files
    ├── App.js               # Main app file
    ├── package.json
    └── .env
```

## 🚀 Setup Instructions

### Step 1: Install Required Software

1. **Install Node.js**
   - Download from: https://nodejs.org/ (get LTS version)
   - Install it on your computer

2. **Install MongoDB**
   - Download from: https://www.mongodb.com/try/download/community
   - Install and keep it running

3. **Install Android Studio**
   - Download from: https://developer.android.com/studio
   - During installation, make sure to install:
     - Android SDK
     - Android SDK Platform
     - Android Virtual Device (AVD)

4. **Setup Java (JDK)**
   - Android Studio will install JDK automatically
   - Or download JDK 11 from: https://www.oracle.com/java/technologies/downloads/

### Step 2: Setup Backend Server

1. **Create project folder**
```bash
mkdir social-media-app
cd social-media-app
mkdir backend
cd backend
```

2. **Initialize Node.js project**
```bash
npm init -y
```

3. **Install backend packages**
```bash
npm install express mongoose bcryptjs jsonwebtoken cors dotenv multer socket.io
npm install nodemon --save-dev
```

4. **Create `.env` file** (in backend folder)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/socialmedia
JWT_SECRET=mysecretkey123456789
```

5. **Update package.json** (add this in scripts section)
```json
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
}
```

6. **Start the server**
```bash
npm run dev
```
Server will run on http://localhost:5000

### Step 3: Setup React Native App

1. **Install React Native CLI**
```bash
npm install -g react-native-cli
```

2. **Create React Native project**
```bash
cd ..
npx react-native init mobile
cd mobile
```

3. **Install app packages**
```bash
npm install @react-navigation/native @react-navigation/stack @react-navigation/bottom-tabs
npm install react-native-screens react-native-safe-area-context
npm install axios socket.io-client
npm install @react-native-async-storage/async-storage
npm install react-native-image-picker
npm install react-native-dotenv
npm install react-native-gesture-handler react-native-reanimated
```

4. **Create `.env` file** (in mobile folder)
```
API_URL=http://10.0.2.2:5000
```
Note: `10.0.2.2` is special IP for Android emulator to reach your computer

5. **Link native dependencies**
```bash
cd android
./gradlew clean
cd ..
```

### Step 4: Run the App

1. **Start Metro (React Native bundler)**
```bash
npm start
```

2. **In a new terminal, run Android app**
```bash
npm run android
```

This will:
- Build the APK
- Install it on emulator/phone
- Launch the app

## 📱 Building APK for Phone

### Build Debug APK (for testing)
```bash
cd android
./gradlew assembleDebug
```
APK location: `android/app/build/outputs/apk/debug/app-debug.apk`

### Build Release APK (for distribution)

1. **Generate a signing key**
```bash
cd android/app
keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

2. **Edit `android/gradle.properties`** (add these lines)
```
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=your_password
MYAPP_RELEASE_KEY_PASSWORD=your_password
```

3. **Edit `android/app/build.gradle`** (add in `android {}` section)
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
        minifyEnabled false
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
}
```

4. **Build release APK**
```bash
cd android
./gradlew assembleRelease
```
APK location: `android/app/build/outputs/apk/release/app-release.apk`

5. **Transfer APK to your phone**
   - Copy the APK file to your phone
   - Open it on your phone to install
   - You may need to enable "Install from Unknown Sources"

## 🔧 Android Permissions

Add to `android/app/src/main/AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

## 📡 API Endpoints

### Auth
- `POST /api/auth/signup` - Create account
- `POST /api/auth/login` - Login

### Posts
- `GET /api/posts` - Get all posts
- `POST /api/posts` - Create post
- `POST /api/posts/:id/like` - Like post
- `POST /api/posts/:id/comment` - Comment on post

### Users
- `GET /api/users/:id` - Get user profile
- `PUT /api/users/profile` - Update profile

### Chat
- `GET /api/chat/:userId` - Get messages
- `POST /api/chat/:userId` - Send message

## 🗄️ Database Models

### User
```javascript
{
  username: String,
  email: String,
  password: String,
  profilePic: String,
  bio: String
}
```

### Post
```javascript
{
  user: ObjectId,
  content: String,
  image: String,
  likes: [ObjectId],
  comments: [{
    user: ObjectId,
    text: String,
    createdAt: Date
  }]
}
```

### Message
```javascript
{
  sender: ObjectId,
  receiver: ObjectId,
  message: String,
  createdAt: Date
}
```

## 🐛 Common Problems & Solutions

### Problem: App won't install
**Solution:** 
- Enable "Install from Unknown Sources" in phone settings
- Make sure you built the APK correctly

### Problem: Can't connect to server
**Solution:**
- For emulator: Use `http://10.0.2.2:5000`
- For real phone: Use your computer's IP like `http://192.168.1.100:5000`
- Make sure phone and computer are on same WiFi
- Check if server is running

### Problem: Images not uploading
**Solution:**
- Check camera/storage permissions in AndroidManifest.xml
- Make sure `uploads` folder exists in backend

### Problem: Build failed
**Solution:**
```bash
cd android
./gradlew clean
cd ..
npm start --reset-cache
npm run android
```

## 📱 Testing on Real Phone

1. **Enable Developer Mode on phone:**
   - Go to Settings > About Phone
   - Tap "Build Number" 7 times
   - Developer options will appear

2. **Enable USB Debugging:**
   - Go to Settings > Developer Options
   - Turn on "USB Debugging"

3. **Connect phone to computer with USB cable**

4. **Check if phone is detected:**
```bash
adb devices
```

5. **Run the app:**
```bash
npm run android
```

## 🌐 Deploy Backend (Optional)

You can deploy your backend to:
- **Heroku** (free tier available)
- **Railway** (free tier available)
- **Render** (free tier available)

Then update your `.env` in mobile app with the deployed URL.

## 📝 Quick Start Checklist

- [ ] Install Node.js
- [ ] Install MongoDB
- [ ] Install Android Studio
- [ ] Setup backend (npm install)
- [ ] Start MongoDB
- [ ] Start backend server (npm run dev)
- [ ] Setup React Native app (npm install)
- [ ] Run app (npm run android)
- [ ] Build APK for phone
- [ ] Install APK on phone

## 💡 Tips

- Always start the backend server before running the app
- Keep MongoDB running in the background
- Use Android emulator for testing first
- Build debug APK for testing, release APK for sharing
- Make sure phone and computer are on same WiFi for real device testing

## 🎯 Next Steps After Setup

1. Create your account in the app
2. Add a profile picture
3. Create your first post
4. Add friends and start chatting!

---

**Need Help?** Check the common problems section or Google the error message you're getting!

**Happy Coding! 🚀**