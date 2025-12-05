# 💊 Medicine Reminder App

A comprehensive cross-platform mobile application built with Flutter that helps users manage their medication schedules with reliable, platform-optimized alarm systems. The app features intelligent notification management, complete CRUD operations, and persistent data storage with backend integration.


## 📱 Screenshots
<p align="center">
  <img src="screenshots/empty_home.png" width="250" />
  <img src="screenshots/home.jpeg" width="250" />
  <img src="screenshots/add_medicine.jpeg" width="250" />
  <img src="screenshots/alarm_screen.jpeg" width="250" />
  <img src="screenshots/notifications.jpeg" width="250" />
  <img src="screenshots/deactive.jpeg" width="250" />
  <img src="screenshots/set_time.jpeg" width="250" />
  <img src="screenshots/user_info.jpeg" width="250" />
</p>


## ✨ Features

### 🔔 Platform-Optimized Alarm System
- **Android**: Full-screen alarms using `alarm` package with guaranteed triggering even when app is killed
- **iOS**: Critical alerts using `awesome_notifications` with high-priority notifications
- Reliable alarm delivery with background execution support
- Automatic alarm rescheduling on system reboot

### 📋 Medicine Management
- ✅ Add multiple medicines with custom names and dosages
- ✏️ Edit existing medicine details and schedules
- 🗑️ Delete medicines with automatic alarm cancellation
- 🔄 Toggle medicine active/inactive status
- 📊 Separate views for active and inactive medicines
- 📅 Set custom end dates for medication courses

### ⏰ Smart Scheduling
- 🕐 Daily medication reminders at specific times
- 🔁 Automatic scheduling from start date to end date
- ⏱️ Snooze functionality (5, 10, 15, 30 minutes)
- 📱 Real-time notification updates
- 🎯 Intelligent alarm ID management to prevent conflicts

### 🔐 Additional Features
- 💾 RESTful API integration with Node.js backend
- 🌐 Real-time data synchronization
- 📱 Responsive Material Design UI
- 🎨 Beautiful gradient interface
- 📊 Medicine tracking and history
- ⚡ Efficient state management with GetX

## 🏗️ Architecture

The project follows a clean architecture pattern with clear separation of concerns:

```
lib/
├── Models/              # Data models
│   └── medicine_model.dart
├── Views/               # UI screens
│   ├── Home_Screen/
│   ├── Add_Medicine_Screen/
│   ├── Edit_Medicine_Screen/
│   └── Alarm_Screen/
├── Controllers/         # Business logic (GetX)
│   ├── home_controller.dart
│   ├── add_medicine_controller.dart
│   ├── edit_medicine_controller.dart
│   └── alarm_controller.dart
├── Services/            # Platform services
│   ├── alarm_service.dart
│   ├── android_alarm_service.dart
│   ├── ios_notification_service.dart
│   ├── unified_notification_service.dart
│   └── medicine_api_service.dart
├── Bindings/            # Dependency injection
├── Routes/              # Navigation
└── Constants/           # App constants
```



## 📦 Dependencies

### Core Dependencies
```yaml
dependencies:
  flutter:
    sdk: flutter
  
  # State Management & Navigation
  get: ^4.6.5
  
  # Platform-Specific Alarms/Notifications
  get: ^4.7.2
  awesome_notifications: ^0.10.1   # iOS notifications 
  alarm: ^5.1.5                    # Android alarms
  
  # Backend Integration
  dio: ^5.3.3                      # HTTP client
  
  # Permissions
  permission_handler: ^11.0.0
```


## ⚙️ Configuration

### Android Configuration

1. **Update `AndroidManifest.xml`**
```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<uses-permission android:name="android.permission.WAKE_LOCK"/>
<uses-permission android:name="android.permission.VIBRATE"/>
<uses-permission android:name="android.permission.USE_FULL_SCREEN_INTENT"/>
<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM"/>
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
<uses-permission android:name="android.permission.USE_EXACT_ALARM"/>
```

2. **Minimum SDK**: API 21 (Android 5.0)
```gradle
minSdkVersion 21
targetSdkVersion 33
```

### iOS Configuration

1. **Update `Info.plist`**
```xml
<key>UIBackgroundModes</key>
<array>
    <string>audio</string>
    <string>processing</string>
</array>
```

2. **Minimum iOS version**: 12.0

## 🎯 Key Features Explained

### Platform-Specific Implementation

The app intelligently uses different packages based on the platform:

- **Android**: Uses the `alarm` package for reliable full-screen alarms that work even when the app is killed
- **iOS**: Uses `awesome_notifications` for critical alerts with high priority

This dual approach ensures optimal user experience on both platforms.

### Alarm ID Management

To prevent conflicts between regular alarms and snoozed alarms:
- Regular alarms: `medicineId × 100000`
- Snooze alarms: `50000000 + (originalAlarmId % 1000000)`

### Smart Cancellation

When medicines are deleted or updated, the app automatically calculates and cancels only the necessary alarms (from current date to end date), instead of blindly canceling 365 days worth of alarms.

## 📊 API Endpoints

The app expects the following REST API endpoints:

```
GET    /medicine-reminder          # Get all medicines
POST   /medicine-reminder          # Create new medicine
PATCH  /medicine-reminder/:id      # Update medicine
DELETE /medicine-reminder/:id      # Delete medicine
```

**Example Medicine Object:**
```json
{
  "id": 1,
  "medicineNames": ["Paracetamol", "Aspirin"],
  "dosage": "500mg",
  "times": {
    "hour": 8,
    "minute": 0
  },
  "intakeTime": "After Food",
  "isActive": true,
  "createdAt": "2024-01-01T00:00:00.000Z",
  "endDate": "2024-12-31T00:00:00.000Z"
}
```



## 👤 Author

**Your Name**
- GitHub: [JubaerFaysal](https://github.com/JubaerFaysal)
- LinkedIn: [Your Name](https://www.linkedin.com/in/jubaer-ahmed-faysal/)
- Email: jubaerfaysal@gmail.com


Made with ❤️ using Flutter
