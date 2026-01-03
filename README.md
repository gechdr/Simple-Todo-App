# ✅ TaskMaster - Kotlin Todo App

<div align="center">

![Android](https://img.shields.io/badge/Android-3DDC84?logo=android&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-1.9.0-7F52FF?logo=kotlin&logoColor=white)
![SDK](https://img.shields.io/badge/SDK-34-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**A multi-user task management Android application with urgency tracking and motivational quotes**

[Features](#-features) • [Screenshots](#-screenshots) • [Installation](#-installation) • [Architecture](#-architecture) • [Contributing](#-contributing)

</div>

---

## 📖 Overview

TaskMaster is a native Android task management application that supports multiple users. Each user can manage their own task list with deadlines, descriptions, and urgency levels. The app features smart sorting options, color-coded urgency indicators, and motivational quotes to keep users inspired.

Built with Kotlin and modern Android development practices including View Binding and RecyclerView with GridLayoutManager.

## ✨ Features

### 👥 Multi-User Support

- **Quick Login** - Enter username to access personal task list
- **Auto Account Creation** - New users automatically get an account
- **Isolated Data** - Each user has their own separate task list

### 📝 Task Management

| Feature | Description |
|---------|-------------|
| **Add Tasks** | Create tasks with name, deadline, description |
| **Urgency Flag** | Mark tasks as urgent with checkbox |
| **Mark Complete** | Remove tasks when done |
| **Grid View** | Tasks displayed in 2-column grid layout |
| **Color Coding** | Urgent tasks highlighted with different color |

### 🔄 Smart Sorting

- **Sort by Deadline** - Order tasks by due date (earliest first)
- **Sort by Urgency** - Urgent tasks first, then by deadline
- **Persistent Sort** - New tasks respect current sort preference

### 💬 Motivational Quotes

Random inspirational quotes from famous personalities:

> *"A goal is a dream with a deadline."* — Napoleon Hill

> *"Quiet people have the loudest minds."* — Stephen Hawking

> *"Fear is stupid. So are regrets."* — Marilyn Monroe

### ✅ Input Validation

- **Required Fields** - All task fields must be filled
- **Date Format** - Validates DD/MM/YYYY format
- **Date Range** - Checks valid day (1-30), month (1-12), year (1000-9999)

## 📱 Screenshots

| Login | Task List | Add Task |
|:---:|:---:|:---:|
| ![Login](screenshots/login.png) | ![Tasks](screenshots/tasks.png) | ![Add](screenshots/add_task.png) |

| Urgent Tasks | Sort Options | Quote |
|:---:|:---:|:---:|
| ![Urgent](screenshots/urgent.png) | ![Sort](screenshots/sort.png) | ![Quote](screenshots/quote.png) |

> **Note**: Add screenshots to the `screenshots/` folder

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| [Kotlin](https://kotlinlang.org/) | Primary programming language |
| [View Binding](https://developer.android.com/topic/libraries/view-binding) | Type-safe view access |
| [RecyclerView](https://developer.android.com/guide/topics/ui/layout/recyclerview) | Efficient list display |
| [GridLayoutManager](https://developer.android.com/reference/androidx/recyclerview/widget/GridLayoutManager) | 2-column grid layout |
| [Material Components](https://material.io/develop/android) | UI components and theming |

## 📋 Requirements

- **Android Studio**: Hedgehog (2023.1.1) or later
- **Minimum SDK**: API 34 (Android 14)
- **Target SDK**: API 34
- **JDK**: 1.8+
- **Gradle**: 8.3.0

## 🚀 Installation

### Clone the Repository

```bash
git clone https://github.com/gechdr/Simple-Todo-App.git
cd Simple-Todo-App
```

### Open in Android Studio

1. Launch **Android Studio**
2. Select **File > Open**
3. Navigate to the cloned repository
4. Click **OK** and wait for Gradle sync

### Build and Run

```bash
# Build the project
./gradlew build

# Install on connected device/emulator
./gradlew installDebug
```

Or click the **Run** button (▶️) in Android Studio.

### Demo Data

The app comes with pre-configured test data:

**Users:**
- `User1` - Has 2 sample tasks
- `User2` - Has 2 sample tasks

Or enter any new username to create a fresh account.

## 📁 Project Structure

```
Kotlin-TodoApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/tugasm4_6958/
│   │   │   │   ├── MainActivity.kt      # Login screen
│   │   │   │   ├── TaskActivity.kt      # Task management
│   │   │   │   ├── QuoteActivity.kt     # Motivational quotes
│   │   │   │   ├── Task.kt              # Task data model
│   │   │   │   ├── TaskAdapter.kt       # RecyclerView adapter
│   │   │   │   └── DB.kt                # In-memory database
│   │   │   │
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml    # Login layout
│   │   │   │   │   ├── activity_task.xml    # Task list layout
│   │   │   │   │   ├── activity_quote.xml   # Quote layout
│   │   │   │   │   └── task_item.xml        # Task card layout
│   │   │   │   ├── drawable/
│   │   │   │   │   └── shape_rounded.xml    # Rounded corners
│   │   │   │   └── values/
│   │   │   │       ├── colors.xml           # Color definitions
│   │   │   │       └── themes.xml           # App theme
│   │   │   │
│   │   │   └── AndroidManifest.xml
│   │   │
│   │   └── test/
│   │
│   └── build.gradle.kts
│
├── gradle/
│   └── libs.versions.toml
│
└── README.md
```

## 🏗️ Architecture

### App Flow

```
┌─────────────────┐
│  MainActivity   │
│    (Login)      │
└────────┬────────┘
         │ Enter username
         ▼
┌─────────────────┐     ┌─────────────────┐
│  TaskActivity   │────▶│  QuoteActivity  │
│  (Task List)    │     │   (Quotes)      │
└─────────────────┘     └─────────────────┘
         │
         ▼
    ┌─────────┐
    │  Task   │
    │  Cards  │
    └─────────┘
```

### Data Model

```kotlin
data class Task(
    val name: String,        // Task title
    val deadline: String,    // Date in DD/MM/YYYY format
    val description: String, // Task details
    val isUrgent: Boolean    // Urgency flag
)
```

### Database Structure

```kotlin
// In-memory storage: Map<Username, List<Task>>
DB.tasks = {
    "User1" -> [Task1, Task2, ...],
    "User2" -> [Task3, Task4, ...],
    ...
}
```

### Sorting Logic

```
Sort by Urgency (Default):
┌──────────────────────────────────────┐
│ 1. Urgent tasks (by deadline)        │
│ 2. Normal tasks (by deadline)        │
└──────────────────────────────────────┘

Sort by Deadline:
┌──────────────────────────────────────┐
│ All tasks ordered by date            │
│ (earliest deadline first)            │
└──────────────────────────────────────┘
```

## 📝 Usage Guide

### Getting Started

1. **Launch App** - Open TaskMaster
2. **Enter Name** - Type your username
3. **Press Enter** - Access your task list

### Adding a Task

1. **Task Name** - Enter a title for your task
2. **Deadline** - Enter date in DD/MM/YYYY format
3. **Description** - Add task details
4. **Urgent** - Check if task is urgent
5. **Add Task** - Press the add button

### Managing Tasks

- **Complete Task** - Press "Done" button on task card
- **Sort by Deadline** - Select deadline radio button
- **Sort by Urgency** - Select urgent radio button
- **Get Inspired** - Press "Quote" for motivation

### Color Coding

| Color | Meaning |
|-------|---------|
| 🔴 Red/Urgent | Task marked as urgent |
| 🟢 Green/Normal | Regular priority task |

## 🔧 Configuration

### Customizing Colors

Edit `app/src/main/res/values/colors.xml`:

```xml
<color name="urgent">#FF5252</color>
<color name="normal">#4CAF50</color>
```

### Adding More Quotes

Edit `QuoteActivity.kt`:

```kotlin
val listQuotes: MutableMap<String,String> = mutableMapOf(
    "Author Name" to "Quote text here.",
    // Add more quotes...
)
```

### Changing Grid Columns

Edit `TaskActivity.kt`:

```kotlin
// Change 2 to desired number of columns
val layoutManager = GridLayoutManager(this, 2)
```

## 🧪 Testing

### Run Unit Tests

```bash
./gradlew test
```

### Run Instrumented Tests

```bash
./gradlew connectedAndroidTest
```

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Feature Ideas

- [ ] Persistent storage with Room Database
- [ ] Task editing functionality
- [ ] Due date notifications
- [ ] Task categories/tags
- [ ] Search and filter tasks
- [ ] Dark mode support
- [ ] Task sharing
- [ ] Recurring tasks
- [ ] Task priority levels (Low/Medium/High)
- [ ] Calendar view
- [ ] Statistics and productivity tracking
- [ ] Cloud sync with Firebase
- [ ] Widget for home screen

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

## 🙏 Acknowledgments

- [Android Developers](https://developer.android.com/) - Official documentation
- [Material Design](https://material.io/) - Design guidelines
- [Kotlin](https://kotlinlang.org/) - Programming language

---

<div align="center">

**Built with Kotlin**

[🔝 Back to Top](#-taskmaster---kotlin-todo-app)

</div>
