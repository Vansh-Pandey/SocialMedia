# Social Media App

A full-stack social media application for Android with features including user authentication, posts, likes, comments, sharing, Q&A, and real-time chat.

## 📱 Features

- **User Authentication**: Secure signup/login with JWT tokens
- **Posts**: Create, edit, and delete posts with images
- **Interactions**: Like, comment, and share posts
- **Q&A Forum**: Ask and answer questions
- **Real-time Chat**: One-on-one messaging
- **User Profiles**: View and edit user profiles
- **Feed**: Personalized content feed
- **Notifications**: Real-time updates for interactions

## 🛠️ Tech Stack

### Backend
- **Node.js** with Express.js
- **MongoDB** with Mongoose ODM
- **Socket.io** for real-time chat
- **JWT** for authentication
- **Multer** for file uploads
- **Bcrypt** for password hashing

### Android Frontend
- **Kotlin**
- **Jetpack Compose** for UI
- **Retrofit** for API calls
- **Room Database** for local caching
- **Coil** for image loading
- **Socket.io Client** for real-time features
- **DataStore** for secure token storage
- **Hilt** for dependency injection

## 📋 Prerequisites

### Backend Development
- Node.js (v16 or higher)
- MongoDB (v5.0 or higher) or MongoDB Atlas account
- npm or yarn package manager

### Android Development
- Android Studio (latest stable version)
- JDK 11 or higher
- Android SDK (API level 24 or higher)
- Gradle 8.0+

## 📁 Project Structure

```
social-media-app/
│
├── backend/                          # Backend server
│   ├── src/
│   │   ├── config/
│   │   │   ├── database.js          # MongoDB connection
│   │   │   ├── cloudinary.js        # Image upload config
│   │   │   └── socket.js            # Socket.io configuration
│   │   │
│   │   ├── models/
│   │   │   ├── User.js              # User schema
│   │   │   ├── Post.js              # Post schema
│   │   │   ├── Comment.js           # Comment schema
│   │   │   ├── Question.js          # Q&A schema
│   │   │   ├── Message.js           # Chat message schema
│   │   │   └── Notification.js      # Notification schema
│   │   │
│   │   ├── controllers/
│   │   │   ├── authController.js    # Authentication logic
│   │   │   ├── postController.js    # Post CRUD operations
│   │   │   ├── userController.js    # User profile operations
│   │   │   ├── questionController.js # Q&A operations
│   │   │   ├── chatController.js    # Chat operations
│   │   │   └── notificationController.js
│   │   │
│   │   ├── routes/
│   │   │   ├── authRoutes.js
│   │   │   ├── postRoutes.js
│   │   │   ├── userRoutes.js
│   │   │   ├── questionRoutes.js
│   │   │   ├── chatRoutes.js
│   │   │   └── notificationRoutes.js
│   │   │
│   │   ├── middleware/
│   │   │   ├── authMiddleware.js    # JWT verification
│   │   │   ├── uploadMiddleware.js  # File upload handling
│   │   │   └── errorMiddleware.js   # Error handling
│   │   │
│   │   ├── utils/
│   │   │   ├── tokenUtils.js        # JWT generation/validation
│   │   │   ├── validators.js        # Input validation
│   │   │   └── helpers.js           # Helper functions
│   │   │
│   │   ├── socket/
│   │   │   ├── chatSocket.js        # Chat socket handlers
│   │   │   └── notificationSocket.js
│   │   │
│   │   └── server.js                # Main entry point
│   │
│   ├── uploads/                     # Uploaded files (local)
│   ├── .env                         # Environment variables
│   ├── .gitignore
│   ├── package.json
│   └── README.md
│
└── android/                          # Android application
    ├── app/
    │   ├── src/
    │   │   ├── main/
    │   │   │   ├── java/com/yourapp/socialmedia/
    │   │   │   │   │
    │   │   │   │   ├── data/
    │   │   │   │   │   ├── local/
    │   │   │   │   │   │   ├── dao/
    │   │   │   │   │   │   │   ├── PostDao.kt
    │   │   │   │   │   │   │   └── UserDao.kt
    │   │   │   │   │   │   ├── database/
    │   │   │   │   │   │   │   └── AppDatabase.kt
    │   │   │   │   │   │   └── preferences/
    │   │   │   │   │   │       └── UserPreferences.kt
    │   │   │   │   │   │
    │   │   │   │   │   ├── remote/
    │   │   │   │   │   │   ├── api/
    │   │   │   │   │   │   │   ├── AuthApi.kt
    │   │   │   │   │   │   │   ├── PostApi.kt
    │   │   │   │   │   │   │   ├── UserApi.kt
    │   │   │   │   │   │   │   ├── QuestionApi.kt
    │   │   │   │   │   │   │   └── ChatApi.kt
    │   │   │   │   │   │   ├── dto/
    │   │   │   │   │   │   │   ├── requests/
    │   │   │   │   │   │   │   └── responses/
    │   │   │   │   │   │   └── socket/
    │   │   │   │   │   │       └── SocketManager.kt
    │   │   │   │   │   │
    │   │   │   │   │   ├── repository/
    │   │   │   │   │   │   ├── AuthRepository.kt
    │   │   │   │   │   │   ├── PostRepository.kt
    │   │   │   │   │   │   ├── UserRepository.kt
    │   │   │   │   │   │   ├── QuestionRepository.kt
    │   │   │   │   │   │   └── ChatRepository.kt
    │   │   │   │   │   │
    │   │   │   │   │   └── models/
    │   │   │   │   │       ├── User.kt
    │   │   │   │   │       ├── Post.kt
    │   │   │   │   │       ├── Comment.kt
    │   │   │   │   │       ├── Question.kt
    │   │   │   │   │       └── Message.kt
    │   │   │   │   │
    │   │   │   │   ├── ui/
    │   │   │   │   │   ├── theme/
    │   │   │   │   │   │   ├── Color.kt
    │   │   │   │   │   │   ├── Theme.kt
    │   │   │   │   │   │   └── Type.kt
    │   │   │   │   │   │
    │   │   │   │   │   ├── components/
    │   │   │   │   │   │   ├── PostCard.kt
    │   │   │   │   │   │   ├── CommentItem.kt
    │   │   │   │   │   │   ├── UserAvatar.kt
    │   │   │   │   │   │   └── LoadingIndicator.kt
    │   │   │   │   │   │
    │   │   │   │   │   ├── screens/
    │   │   │   │   │   │   ├── auth/
    │   │   │   │   │   │   │   ├── LoginScreen.kt
    │   │   │   │   │   │   │   └── SignupScreen.kt
    │   │   │   │   │   │   ├── home/
    │   │   │   │   │   │   │   ├── HomeScreen.kt
    │   │   │   │   │   │   │   └── FeedScreen.kt
    │   │   │   │   │   │   ├── post/
    │   │   │   │   │   │   │   ├── CreatePostScreen.kt
    │   │   │   │   │   │   │   └── PostDetailScreen.kt
    │   │   │   │   │   │   ├── profile/
    │   │   │   │   │   │   │   ├── ProfileScreen.kt
    │   │   │   │   │   │   │   └── EditProfileScreen.kt
    │   │   │   │   │   │   ├── question/
    │   │   │   │   │   │   │   ├── QuestionListScreen.kt
    │   │   │   │   │   │   │   ├── AskQuestionScreen.kt
    │   │   │   │   │   │   │   └── QuestionDetailScreen.kt
    │   │   │   │   │   │   └── chat/
    │   │   │   │   │   │       ├── ChatListScreen.kt
    │   │   │   │   │   │       └── ChatScreen.kt
    │   │   │   │   │   │
    │   │   │   │   │   └── navigation/
    │   │   │   │   │       └── NavGraph.kt
    │   │   │   │   │
    │   │   │   │   ├── viewmodel/
    │   │   │   │   │   ├── AuthViewModel.kt
    │   │   │   │   │   ├── PostViewModel.kt
    │   │   │   │   │   ├── UserViewModel.kt
    │   │   │   │   │   ├── QuestionViewModel.kt
    │   │   │   │   │   └── ChatViewModel.kt
    │   │   │   │   │
    │   │   │   │   ├── di/
    │   │   │   │   │   ├── AppModule.kt
    │   │   │   │   │   ├── NetworkModule.kt
    │   │   │   │   │   └── DatabaseModule.kt
    │   │   │   │   │
    │   │   │   │   ├── utils/
    │   │   │   │   │   ├── Constants.kt
    │   │   │   │   │   ├── Extensions.kt
    │   │   │   │   │   └── Resource.kt
    │   │   │   │   │
    │   │   │   │   └── MainActivity.kt
    │   │   │   │
    │   │   │   ├── res/
    │   │   │   │   ├── drawable/
    │   │   │   │   ├── values/
    │   │   │   │   │   ├── colors.xml
    │   │   │   │   │   ├── strings.xml
    │   │   │   │   │   └── themes.xml
    │   │   │   │   └── xml/
    │   │   │   │       └── network_security_config.xml
    │   │   │   │
    │   │   │   └── AndroidManifest.xml
    │   │   │
    │   │   └── test/
    │   │       └── java/
    │   │
    │   ├── build.gradle.kts
    │   └── proguard-rules.pro
    │
    ├── gradle/
    ├── build.gradle.kts
    ├── settings.gradle.kts
    ├── gradle.properties
    └── README.md
```

## 🚀 Getting Started

### Backend Setup

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd social-media-app/backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Create `.env` file in the backend directory**
```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=mongodb://localhost:27017/socialmedia
# Or use MongoDB Atlas:
# MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/socialmedia

# JWT Secret
JWT_SECRET=your_super_secret_jwt_key_here_change_this
JWT_EXPIRE=7d

# File Upload (Optional - for Cloudinary)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# CORS
CLIENT_URL=http://localhost:3000
```

4. **Start MongoDB** (if running locally)
```bash
# macOS/Linux
mongod

# Windows
"C:\Program Files\MongoDB\Server\5.0\bin\mongod.exe"
```

5. **Run the backend server**
```bash
# Development mode with auto-restart
npm run dev

# Production mode
npm start
```

The backend server will start at `http://localhost:5000`

### Android Setup

1. **Open Android Studio**
   - Open Android Studio
   - Select "Open an Existing Project"
   - Navigate to `social-media-app/android`

2. **Update API Base URL**
   
   Open `app/src/main/java/com/yourapp/socialmedia/utils/Constants.kt` and update:
   ```kotlin
   object Constants {
       // For emulator
       const val BASE_URL = "http://10.0.2.2:5000/api/"
       
       // For physical device (use your computer's IP)
       // const val BASE_URL = "http://192.168.1.XXX:5000/api/"
   }
   ```

3. **Sync Gradle files**
   - Wait for Gradle sync to complete
   - Resolve any dependency issues

4. **Run the app**
   - Connect an Android device or start an emulator
   - Click the "Run" button in Android Studio
   - Select your device/emulator

## 📦 Dependencies

### Backend Dependencies
```json
{
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.5.0",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.2",
    "socket.io": "^4.7.2",
    "multer": "^1.4.5-lts.1",
    "cloudinary": "^1.41.0",
    "dotenv": "^16.3.1",
    "cors": "^2.8.5",
    "express-validator": "^7.0.1",
    "helmet": "^7.0.0",
    "morgan": "^1.10.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

### Android Dependencies (in `build.gradle.kts`)
```kotlin
dependencies {
    // Core Android
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")
    
    // Compose
    implementation("androidx.activity:activity-compose:1.8.2")
    implementation(platform("androidx.compose:compose-bom:2024.01.00"))
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.material3:material3")
    implementation("androidx.compose.ui:ui-tooling-preview")
    
    // Navigation
    implementation("androidx.navigation:navigation-compose:2.7.6")
    
    // Retrofit for API calls
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.12.0")
    
    // Socket.io
    implementation("io.socket:socket.io-client:2.1.0")
    
    // Room Database
    implementation("androidx.room:room-runtime:2.6.1")
    implementation("androidx.room:room-ktx:2.6.1")
    kapt("androidx.room:room-compiler:2.6.1")
    
    // Hilt for Dependency Injection
    implementation("com.google.dagger:hilt-android:2.50")
    kapt("com.google.dagger:hilt-compiler:2.50")
    implementation("androidx.hilt:hilt-navigation-compose:1.1.0")
    
    // Coil for Image Loading
    implementation("io.coil-kt:coil-compose:2.5.0")
    
    // DataStore
    implementation("androidx.datastore:datastore-preferences:1.0.0")
    
    // ViewModel
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.7.0")
}
```

## 🔧 Configuration

### Network Security (Android)

Create `res/xml/network_security_config.xml` to allow HTTP connections in development:

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="system" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

Add to `AndroidManifest.xml`:
```xml
<application
    android:networkSecurityConfig="@xml/network_security_config"
    ...>
```

### Permissions (Android)

Add to `AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.CAMERA" />
```

## 📡 API Endpoints

### Authentication
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Posts
- `GET /api/posts` - Get all posts
- `POST /api/posts` - Create new post
- `GET /api/posts/:id` - Get single post
- `PUT /api/posts/:id` - Update post
- `DELETE /api/posts/:id` - Delete post
- `POST /api/posts/:id/like` - Like/unlike post
- `POST /api/posts/:id/comment` - Add comment
- `POST /api/posts/:id/share` - Share post

### Questions
- `GET /api/questions` - Get all questions
- `POST /api/questions` - Ask question
- `GET /api/questions/:id` - Get question details
- `POST /api/questions/:id/answer` - Post answer

### Chat
- `GET /api/chat/conversations` - Get user's conversations
- `GET /api/chat/:userId` - Get chat with specific user
- `POST /api/chat/:userId` - Send message

### Users
- `GET /api/users/:id` - Get user profile
- `PUT /api/users/:id` - Update profile
- `GET /api/users/:id/posts` - Get user's posts

## 🔐 Authentication Flow

1. User signs up or logs in
2. Backend validates credentials and returns JWT token
3. Android app stores token in DataStore
4. Token is included in Authorization header for subsequent requests
5. Backend middleware verifies token for protected routes

## 💾 Database Schema

### User Model
```javascript
{
  username: String (unique),
  email: String (unique),
  password: String (hashed),
  fullName: String,
  bio: String,
  profilePicture: String,
  followers: [ObjectId],
  following: [ObjectId],
  createdAt: Date
}
```

### Post Model
```javascript
{
  user: ObjectId (ref: User),
  content: String,
  images: [String],
  likes: [ObjectId],
  comments: [{
    user: ObjectId,
    text: String,
    createdAt: Date
  }],
  shares: Number,
  createdAt: Date
}
```

### Message Model
```javascript
{
  sender: ObjectId (ref: User),
  recipient: ObjectId (ref: User),
  content: String,
  read: Boolean,
  createdAt: Date
}
```

## 🧪 Testing

### Backend Testing
```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage
```

### Android Testing
```bash
# Run unit tests
./gradlew test

# Run instrumentation tests
./gradlew connectedAndroidTest
```

## 🔨 Building for Production

### Backend
```bash
# Set environment to production
NODE_ENV=production

# Use process manager like PM2
npm install -g pm2
pm2 start src/server.js --name social-media-api
```

### Android
1. Generate signed APK/Bundle in Android Studio
2. Build > Generate Signed Bundle/APK
3. Follow the wizard to create keystore and build

## 🐛 Common Issues & Solutions

### Issue: Cannot connect to backend from Android
- **Solution**: Make sure you're using the correct IP address
  - Emulator: Use `10.0.2.2` instead of `localhost`
  - Physical device: Use your computer's local IP address

### Issue: MongoDB connection failed
- **Solution**: 
  - Ensure MongoDB is running
  - Check connection string in `.env`
  - Verify network access if using MongoDB Atlas

### Issue: Socket.io not connecting
- **Solution**:
  - Check CORS settings in backend
  - Verify socket URL in Android app
  - Ensure server is running

### Issue: Images not uploading
- **Solution**:
  - Check file size limits in Multer configuration
  - Verify Cloudinary credentials
  - Ensure proper permissions in AndroidManifest.xml

## 📱 Features to Implement Next

- [ ] Push notifications using FCM
- [ ] Stories feature
- [ ] Video posts
- [ ] Live streaming
- [ ] Groups/Communities
- [ ] Advanced search
- [ ] Content moderation
- [ ] Analytics dashboard

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support

For issues and questions:
- Create an issue in the GitHub repository
- Email: support@yourapp.com

## 🙏 Acknowledgments

- Node.js and Express.js communities
- Android Jetpack Compose team
- MongoDB team
- All open-source contributors

---

**Happy Coding! 🚀**