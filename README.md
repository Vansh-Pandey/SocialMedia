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
**Development:** VS Code (No Android Studio needed!)

## 📁 Project Structure

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

---

# 🚀 COMPLETE SETUP GUIDE - FROM ZERO TO TESTING

## PART 1: Install Required Software

### Step 1.1: Install Node.js

1. Go to https://nodejs.org/
2. Download LTS version (recommended)
3. Run installer and follow the steps
4. Verify installation:
```bash
node --version
npm --version
```
You should see version numbers like v18.x.x and 9.x.x

### Step 1.2: Install VS Code

1. Go to https://code.visualstudio.com/
2. Download and install
3. Open VS Code
4. Install these extensions (click Extensions icon on left):
   - ES7+ React/Redux/React-Native snippets
   - React Native Tools
   - ESLint
   - Prettier

### Step 1.3: Install MongoDB

**Windows:**
1. Go to https://www.mongodb.com/try/download/community
2. Download MongoDB Community Server
3. Run installer (choose "Complete" installation)
4. Check "Install MongoDB as a Service"
5. Install MongoDB Compass (GUI tool) when prompted

**Mac:**
```bash
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
```

**Linux (Ubuntu/Debian):**
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod
```

Verify MongoDB:
```bash
mongosh
```
You should see MongoDB shell. Type `exit` to quit.

### Step 1.4: Install Java Development Kit (JDK)

**Windows/Mac/Linux:**
1. Go to https://adoptium.net/
2. Download JDK 11 or JDK 17 (LTS versions)
3. Install and follow the steps
4. Verify:
```bash
java -version
```

**Or use Chocolatey (Windows):**
```bash
choco install microsoft-openjdk17
```

**Or use Homebrew (Mac):**
```bash
brew install openjdk@17
```

### Step 1.5: Install Android SDK (WITHOUT Android Studio)

We'll use command-line tools only!

**Download Android Command Line Tools:**

1. Go to https://developer.android.com/studio#command-tools
2. Scroll down to "Command line tools only"
3. Download for your OS (Windows/Mac/Linux)
4. Extract the zip file

**Setup on Windows:**
```bash
# Create Android folder
mkdir C:\Android
cd C:\Android

# Extract command line tools to: C:\Android\cmdline-tools\latest\

# Set environment variables (search "Environment Variables" in Windows)
# Add these:
ANDROID_HOME = C:\Android
JAVA_HOME = C:\Program Files\Eclipse Adoptium\jdk-17.x.x-hotspot

# Add to PATH:
%ANDROID_HOME%\cmdline-tools\latest\bin
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
%JAVA_HOME%\bin
```

**Setup on Mac/Linux:**
```bash
# Create Android folder
mkdir -p ~/Android/cmdline-tools
cd ~/Android/cmdline-tools

# Extract the downloaded zip here and rename to 'latest'
# You should have: ~/Android/cmdline-tools/latest/

# Add to ~/.bash_profile or ~/.zshrc:
export ANDROID_HOME=$HOME/Android
export JAVA_HOME=$(/usr/libexec/java_home)  # Mac
# export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64  # Linux

export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator

# Reload:
source ~/.bash_profile  # or source ~/.zshrc
```

**Install Android SDK packages:**
```bash
# Accept licenses
sdkmanager --licenses

# Install required packages
sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.0"
sdkmanager "system-images;android-33;google_apis;x86_64"
```

Verify:
```bash
adb --version
sdkmanager --list
```

---

## PART 2: Create the Project

### Step 2.1: Create Project Folder Structure

Open VS Code terminal (View > Terminal or Ctrl + `)

```bash
# Create main project folder
mkdir social-media-app
cd social-media-app

# Open in VS Code
code .
```

### Step 2.2: Setup Backend

```bash
# Create backend folder
mkdir backend
cd backend

# Initialize Node.js project
npm init -y

# Install dependencies
npm install express mongoose bcryptjs jsonwebtoken cors dotenv multer socket.io

# Install dev dependencies
npm install nodemon --save-dev
```

**Create folder structure:**
```bash
mkdir models routes middleware uploads
```

**Create `.env` file in backend folder:**
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/socialmedia
JWT_SECRET=your_super_secret_key_change_this_in_production
```

**Update `package.json`** - Add to scripts:
```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

### Step 2.3: Create Backend Files

I'll provide all backend code files. Create these files in VS Code:

**backend/server.js:**
```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const dotenv = require('dotenv');
const http = require('http');
const socketIo = require('socket.io');

dotenv.config();

const app = express();
const server = http.createServer(app);
const io = socketIo(server, {
  cors: {
    origin: "*",
    methods: ["GET", "POST"]
  }
});

// Middleware
app.use(cors());
app.use(express.json());
app.use('/uploads', express.static('uploads'));

// MongoDB Connection
mongoose.connect(process.env.MONGODB_URI)
  .then(() => console.log('✅ MongoDB Connected'))
  .catch(err => console.log('❌ MongoDB Error:', err));

// Routes
app.use('/api/auth', require('./routes/auth'));
app.use('/api/posts', require('./routes/posts'));
app.use('/api/users', require('./routes/users'));
app.use('/api/chat', require('./routes/chat'));

// Socket.IO for real-time chat
io.on('connection', (socket) => {
  console.log('User connected:', socket.id);

  socket.on('join', (userId) => {
    socket.join(userId);
    console.log(`User ${userId} joined their room`);
  });

  socket.on('send_message', (data) => {
    io.to(data.receiverId).emit('receive_message', data);
  });

  socket.on('disconnect', () => {
    console.log('User disconnected:', socket.id);
  });
});

// Start server
const PORT = process.env.PORT || 5000;
server.listen(PORT, () => {
  console.log(`🚀 Server running on http://localhost:${PORT}`);
});
```

**backend/models/User.js:**
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true,
    trim: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true
  },
  password: {
    type: String,
    required: true
  },
  profilePic: {
    type: String,
    default: ''
  },
  bio: {
    type: String,
    default: ''
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

module.exports = mongoose.model('User', userSchema);
```

**backend/models/Post.js:**
```javascript
const mongoose = require('mongoose');

const commentSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  text: {
    type: String,
    required: true
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

const postSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  content: {
    type: String,
    required: true
  },
  image: {
    type: String,
    default: ''
  },
  likes: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User'
  }],
  comments: [commentSchema],
  createdAt: {
    type: Date,
    default: Date.now
  }
});

module.exports = mongoose.model('Post', postSchema);
```

**backend/models/Message.js:**
```javascript
const mongoose = require('mongoose');

const messageSchema = new mongoose.Schema({
  sender: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  receiver: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  message: {
    type: String,
    required: true
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

module.exports = mongoose.model('Message', messageSchema);
```

**backend/middleware/auth.js:**
```javascript
const jwt = require('jsonwebtoken');

module.exports = (req, res, next) => {
  try {
    const token = req.header('Authorization')?.replace('Bearer ', '');
    
    if (!token) {
      return res.status(401).json({ message: 'No authentication token' });
    }

    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.userId = decoded.userId;
    next();
  } catch (error) {
    res.status(401).json({ message: 'Invalid token' });
  }
};
```

**backend/routes/auth.js:**
```javascript
const express = require('express');
const router = express.Router();
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const User = require('../models/User');

// Signup
router.post('/signup', async (req, res) => {
  try {
    const { username, email, password } = req.body;

    // Check if user exists
    const existingUser = await User.findOne({ $or: [{ email }, { username }] });
    if (existingUser) {
      return res.status(400).json({ message: 'User already exists' });
    }

    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);

    // Create user
    const user = new User({
      username,
      email,
      password: hashedPassword
    });

    await user.save();

    // Create token
    const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET);

    res.status(201).json({
      token,
      user: {
        id: user._id,
        username: user.username,
        email: user.email,
        profilePic: user.profilePic,
        bio: user.bio
      }
    });
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Login
router.post('/login', async (req, res) => {
  try {
    const { email, password } = req.body;

    // Find user
    const user = await User.findOne({ email });
    if (!user) {
      return res.status(400).json({ message: 'Invalid credentials' });
    }

    // Check password
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) {
      return res.status(400).json({ message: 'Invalid credentials' });
    }

    // Create token
    const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET);

    res.json({
      token,
      user: {
        id: user._id,
        username: user.username,
        email: user.email,
        profilePic: user.profilePic,
        bio: user.bio
      }
    });
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

module.exports = router;
```

**backend/routes/posts.js:**
```javascript
const express = require('express');
const router = express.Router();
const Post = require('../models/Post');
const auth = require('../middleware/auth');
const multer = require('multer');
const path = require('path');

// Multer config for image upload
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, 'uploads/');
  },
  filename: (req, file, cb) => {
    cb(null, Date.now() + path.extname(file.originalname));
  }
});

const upload = multer({ storage });

// Get all posts
router.get('/', auth, async (req, res) => {
  try {
    const posts = await Post.find()
      .populate('user', 'username profilePic')
      .populate('comments.user', 'username profilePic')
      .sort({ createdAt: -1 });
    res.json(posts);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Create post
router.post('/', auth, upload.single('image'), async (req, res) => {
  try {
    const { content } = req.body;
    const image = req.file ? `/uploads/${req.file.filename}` : '';

    const post = new Post({
      user: req.userId,
      content,
      image
    });

    await post.save();
    await post.populate('user', 'username profilePic');

    res.status(201).json(post);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Like post
router.post('/:id/like', auth, async (req, res) => {
  try {
    const post = await Post.findById(req.params.id);
    
    if (!post) {
      return res.status(404).json({ message: 'Post not found' });
    }

    const likeIndex = post.likes.indexOf(req.userId);
    
    if (likeIndex === -1) {
      post.likes.push(req.userId);
    } else {
      post.likes.splice(likeIndex, 1);
    }

    await post.save();
    res.json(post);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Comment on post
router.post('/:id/comment', auth, async (req, res) => {
  try {
    const { text } = req.body;
    const post = await Post.findById(req.params.id);

    if (!post) {
      return res.status(404).json({ message: 'Post not found' });
    }

    post.comments.push({
      user: req.userId,
      text
    });

    await post.save();
    await post.populate('comments.user', 'username profilePic');

    res.json(post);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

module.exports = router;
```

**backend/routes/users.js:**
```javascript
const express = require('express');
const router = express.Router();
const User = require('../models/User');
const auth = require('../middleware/auth');
const multer = require('multer');
const path = require('path');

const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, 'uploads/');
  },
  filename: (req, file, cb) => {
    cb(null, Date.now() + path.extname(file.originalname));
  }
});

const upload = multer({ storage });

// Get user profile
router.get('/:id', auth, async (req, res) => {
  try {
    const user = await User.findById(req.params.id).select('-password');
    if (!user) {
      return res.status(404).json({ message: 'User not found' });
    }
    res.json(user);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Update profile
router.put('/profile', auth, upload.single('profilePic'), async (req, res) => {
  try {
    const { username, bio } = req.body;
    const updateData = { username, bio };

    if (req.file) {
      updateData.profilePic = `/uploads/${req.file.filename}`;
    }

    const user = await User.findByIdAndUpdate(
      req.userId,
      updateData,
      { new: true }
    ).select('-password');

    res.json(user);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Search users
router.get('/search/:query', auth, async (req, res) => {
  try {
    const users = await User.find({
      username: { $regex: req.params.query, $options: 'i' }
    }).select('-password').limit(10);
    res.json(users);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

module.exports = router;
```

**backend/routes/chat.js:**
```javascript
const express = require('express');
const router = express.Router();
const Message = require('../models/Message');
const auth = require('../middleware/auth');

// Get messages with a user
router.get('/:userId', auth, async (req, res) => {
  try {
    const messages = await Message.find({
      $or: [
        { sender: req.userId, receiver: req.params.userId },
        { sender: req.params.userId, receiver: req.userId }
      ]
    }).sort({ createdAt: 1 });

    res.json(messages);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

// Send message
router.post('/:userId', auth, async (req, res) => {
  try {
    const { message } = req.body;

    const newMessage = new Message({
      sender: req.userId,
      receiver: req.params.userId,
      message
    });

    await newMessage.save();
    res.status(201).json(newMessage);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

module.exports = router;
```

### Step 2.4: Test Backend

```bash
# Make sure you're in backend folder
cd backend

# Start MongoDB (if not running)
# Windows: Start MongoDB service from Services
# Mac: brew services start mongodb-community
# Linux: sudo systemctl start mongod

# Start backend server
npm run dev
```

You should see:
```
✅ MongoDB Connected
🚀 Server running on http://localhost:5000
```

Test with browser: http://localhost:5000
(You should see "Cannot GET /" which is normal)

---

## PART 3: Setup React Native App

### Step 3.1: Create React Native Project

```bash
# Go back to main project folder
cd ..

# Create React Native app
npx react-native@latest init mobile

# Navigate to mobile folder
cd mobile
```

### Step 3.2: Install Dependencies

```bash
# Navigation
npm install @react-navigation/native @react-navigation/stack @react-navigation/bottom-tabs
npm install react-native-screens react-native-safe-area-context react-native-gesture-handler react-native-reanimated

# API and Storage
npm install axios socket.io-client
npm install @react-native-async-storage/async-storage

# Image picker
npm install react-native-image-picker

# Environment variables
npm install react-native-dotenv

# For Android
cd android
./gradlew clean
cd ..
```

**Windows users:** If `./gradlew` doesn't work, use:
```bash
cd android
gradlew.bat clean
cd ..
```

### Step 3.3: Configure React Native

**Create `.env` file in mobile folder:**
```env
API_URL=http://10.0.2.2:5000
```

**Update `babel.config.js`:**
```javascript
module.exports = {
  presets: ['module:metro-react-native-babel-preset'],
  plugins: [
    [
      'module:react-native-dotenv',
      {
        moduleName: '@env',
        path: '.env',
      },
    ],
    'react-native-reanimated/plugin',
  ],
};
```

**Update `android/app/src/main/AndroidManifest.xml`** - Add permissions before `<application>`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" android:maxSdkVersion="32" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="32" />
```

Also add this attribute to `<application>` tag:
```xml
android:usesCleartextTraffic="true"
```

### Step 3.4: Create App Folder Structure

```bash
# Make sure you're in mobile folder
mkdir -p src/screens src/components src/api src/navigation src/utils
```

---

## PART 4: Build the React Native App

Due to length constraints, I'll provide a starter template for the main files:

**mobile/src/api/api.js:**
```javascript
import axios from 'axios';
import AsyncStorage from '@react-native-async-storage/async-storage';
import { API_URL } from '@env';

const api = axios.create({
  baseURL: API_URL || 'http://10.0.2.2:5000',
  timeout: 10000,
});

// Add token to requests
api.interceptors.request.use(
  async (config) => {
    const token = await AsyncStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

export default api;
```

**mobile/src/utils/storage.js:**
```javascript
import AsyncStorage from '@react-native-async-storage/async-storage';

export const saveToken = async (token) => {
  await AsyncStorage.setItem('token', token);
};

export const getToken = async () => {
  return await AsyncStorage.getItem('token');
};

export const removeToken = async () => {
  await AsyncStorage.removeItem('token');
};

export const saveUser = async (user) => {
  await AsyncStorage.setItem('user', JSON.stringify(user));
};

export const getUser = async () => {
  const user = await AsyncStorage.getItem('user');
  return user ? JSON.parse(user) : null;
};

export const removeUser = async () => {
  await AsyncStorage.removeItem('user');
};
```

**mobile/App.js:**
```javascript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import LoginScreen from './src/screens/LoginScreen';
import SignupScreen from './src/screens/SignupScreen';
import HomeScreen from './src/screens/HomeScreen';

const Stack = createStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Login">
        <Stack.Screen name="Login" component={LoginScreen} />
        <Stack.Screen name="Signup" component={SignupScreen} />
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

**mobile/src/screens/LoginScreen.js** (Simple version):
```javascript
import React, { useState } from 'react';
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  StyleSheet,
  Alert,
} from 'react-native';
import api from '../api/api';
import { saveToken, saveUser } from '../utils/storage';

const LoginScreen = ({ navigation }) => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [loading, setLoading] = useState(false);

  const handleLogin = async () => {
    if (!email || !password) {
      Alert.alert('Error', 'Please fill all fields');
      return;
    }

    try {
      setLoading(true);
      const response = await api.post('/api/auth/login', { email, password });
      await saveToken(response.data.token);
      await saveUser(response.data.user);
      navigation.replace('Home');
    } catch (error) {
      Alert.alert('Error', error.response?.data?.message || 'Login failed');
    } finally {
      setLoading(false);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Social Media App</Text>
      <TextInput
        style={styles.input}
        placeholder="Email"
        value={email}
        onChangeText={setEmail}
        autoCapitalize="none"
        keyboardType="email-address"
      />
      <TextInput
        style={styles.input}
        placeholder="Password"
        value={password}
        onChangeText={setPassword}
        secureTextEntry
      />
      <TouchableOpacity
        style={styles.button}
        onPress={handleLogin}
        disabled={loading}
      >
        <Text style={styles.buttonText}>
          {loading ? 'Loading...' : 'Login'}
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={() => navigation.navigate('Signup')}>
        <Text style={styles.link}>Don't have an account? Sign up</Text>
      </TouchableOpacity>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    padding: 20,
    backgroundColor: '#fff',
  },
  title: {
    fontSize: 32,
    fontWeight: 'bold',
    marginBottom: 40,
    textAlign: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ddd',
    padding: 15,
    marginBottom: 15,
    borderRadius: 8,
  },
  button: {
    backgroundColor: '#007AFF',
    padding: 15,
    borderRadius: 8,
    marginTop: 10,
  },
  buttonText: {
    color: '#fff',
    textAlign: 'center',
    fontSize: 16,
    fontWeight: 'bold',
  },
  link: {
    color: '#007AFF',
    textAlign: 'center',
    marginTop: 20,
  },
});

export default LoginScreen;
```

---

## PART 5: Running and Testing

### Step 5.1: Start Backend Server

```bash
# Terminal 1 - Backend
cd backend
npm run dev
```

Keep this running.

### Step 5.2: Setup Android Emulator (Command Line)

**Create an Android Virtual Device:**
```bash
# List available system images
avdmanager list

# Create AVD
avdmanager create avd -n TestDevice -k "system-images;android-33;google_apis;x86_64" -d "pixel_5"

# List your AVDs
emulator -list-avds

# Start emulator
emulator -avd TestDevice
```

**Alternative - Use your physical Android phone:**
1. Enable Developer Mode (tap Build Number 7 times in Settings > About Phone)
2. Enable USB Debugging in Developer Options
3. Connect phone via USB
4. Check connection: `adb devices`

### Step 5.3: Run React Native App

```bash
# Terminal 2 - React Native Metro
cd mobile
npx react-native start
```

```bash
# Terminal 3 - Run on Android
cd mobile
npx react-native run-android
```

### Step 5.4: Testing Checklist

**Backend Tests:**
- [ ] Server starts without errors
- [ ] MongoDB connection successful
- [ ] Can access http://localhost:5000

**App Tests:**
- [ ] App installs on emulator/device
- [ ] Login screen appears
- [ ] Can navigate to signup screen
- [ ] Backend API connection works

**Manual Testing Steps:**

1. **Test Signup:**
   - Open app
   - Go to Signup
   - Create account with: username, email, password
   - Should redirect to Home

2. **Test Login:**
   - Logout (you'll add this later)
   - Login with created credentials
   - Should redirect to Home

3. **Test Backend API with Postman/Thunder Client:**

Install Thunder Client extension in VS Code, then test:

```
POST http://localhost:5000/api/auth/signup
Body (JSON):
{
  "username": "testuser",
  "email": "test@example.com",
  "password": "password123"
}
```

---

## PART 6: Building APK

### For Testing (Debug APK):

```bash
cd mobile/android
./gradlew assembleDebug
```

APK location: `mobile/android/app/build/outputs/apk/debug/app-debug.apk`

### For Release (Production APK):

1. **Generate signing key:**
```bash
cd mobile/android/app
keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

2. **Edit `mobile/android/gradle.properties`** (add at end):
```properties
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=your_password_here
MYAPP_RELEASE_KEY_PASSWORD=your_password_here
```

3. **Edit `mobile/android/app/build.gradle`** (add in `android {}` block):
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

4. **Build release APK:**
```bash
cd mobile/android
./gradlew assembleRelease
```

APK location: `mobile/android/app/build/outputs/apk/release/app-release.apk`

5. **Install on phone:**
   - Transfer APK to phone
   - Enable "Install Unknown Apps" in Settings
   - Install APK

---

## 🔧 Common Issues & Solutions

### Issue: "SDK location not found"
**Solution:**
Create `mobile/android/local.properties`:
```
sdk.dir=/path/to/your/Android
# Windows: sdk.dir=C:\\Android
# Mac: sdk.dir=/Users/yourname/Android
# Linux: sdk.dir=/home/yourname/Android
```

### Issue: "Unable to connect to server"
**Solution:**
- For emulator: Use `http://10.0.2.2:5000`
- For real device: Use your computer's local IP
  - Find IP: `ipconfig` (Windows) or `ifconfig` (Mac/Linux)
  - Use: `http://192.168.1.XXX:5000`
  - Update `.env` file in mobile folder

### Issue: "Command not found: adb/sdkmanager"
**Solution:** 
Check environment variables are set correctly and restart terminal/VS Code

### Issue: Build fails with Gradle error
**Solution:**
```bash
cd mobile/android
./gradlew clean
cd ../..
npx react-native start --reset-cache
```

### Issue: App crashes on startup
**Solution:**
Check backend is running and API_URL in `.env` is correct

### Issue: Metro bundler error
**Solution:**
```bash
cd mobile
npx react-native start --reset-cache
```

---

## 📱 Quick Start Commands Reference

**Start Backend:**
```bash
cd backend
npm run dev
```

**Start Metro Bundler:**
```bash
cd mobile
npx react-native start
```

**Run on Android:**
```bash
cd mobile
npx react-native run-android
```

**Build Debug APK:**
```bash
cd mobile/android
./gradlew assembleDebug
```

**Build Release APK:**
```bash
cd mobile/android
./gradlew assembleRelease
```

---

## 🎯 Next Steps

After you have the basic app running:

1. Complete all screen components (HomeScreen, CreatePostScreen, etc.)
2. Add proper error handling
3. Implement image upload functionality
4. Add real-time chat with Socket.IO
5. Improve UI/UX with better styling
6. Add loading states and animations
7. Test on multiple devices
8. Deploy backend to cloud (Heroku/Railway/Render)

---

## 📚 Useful VS Code Extensions

- ES7+ React/Redux/React-Native snippets
- React Native Tools
- ESLint
- Prettier
- Thunder Client (for API testing)
- GitLens (if using Git)
- Error Lens (see errors inline)

---

## 🆘 Getting Help

- Check terminal for error messages
- Use VS Code's built-in debugger
- Test backend with Thunder Client
- Check React Native logs: `npx react-native log-android`
- Google specific error messages

---

**Happy Coding! 🚀**

Built with ❤️ using VS Code and command-line tools only!