# README 7: How to Create a New Screen in Flutter

---

## Introduction

In Flutter, a **screen** (also known as a “page” or “route”) is typically represented by a widget—most often a `StatelessWidget` or `StatefulWidget`. Creating a new screen is essential for building multi-page apps (like login, signup, dashboard, etc.). Unlike Android (where screens are Activities/Fragments with XML layouts), Flutter screens are Dart files containing widget trees.

---

## Detailed Explanation

### Step 1: **Create a New Dart File for the Screen**

- Professional convention is to store screens in a `lib/screens/` directory for clarity and scalability.
- Example: Create a file named `profile_screen.dart`.

```dart
// lib/screens/profile_screen.dart
import 'package:flutter/material.dart';

class ProfileScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Profile')),
      body: Center(child: Text('This is the profile screen')),
    );
  }
}
```

### Step 2: **Define the Screen as a Widget**

- Use `StatelessWidget` if the UI won’t change (no internal state).
- Use `StatefulWidget` if the UI will update based on user actions or data.

**Stateless Example:**
```dart
class AboutScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('About')),
      body: Center(child: Text('About the app')),
    );
  }
}
```

**Stateful Example:**
```dart
class SettingsScreen extends StatefulWidget {
  @override
  State<SettingsScreen> createState() => _SettingsScreenState();
}

class _SettingsScreenState extends State<SettingsScreen> {
  bool notificationsEnabled = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: SwitchListTile(
        title: Text('Enable Notifications'),
        value: notificationsEnabled,
        onChanged: (val) {
          setState(() {
            notificationsEnabled = val;
          });
        },
      ),
    );
  }
}
```

### Step 3: **Navigate to the New Screen**

- Use Flutter’s navigation system to move between screens.

**Push a new screen:**
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => ProfileScreen()),
);
```

**Named routes (recommended for larger apps):**
1. Register routes in your `MaterialApp`:
   ```dart
   MaterialApp(
     routes: {
       '/profile': (context) => ProfileScreen(),
       '/settings': (context) => SettingsScreen(),
     },
   )
   ```
2. Navigate using:
   ```dart
   Navigator.pushNamed(context, '/profile');
   ```

### Step 4: **Pass Data between Screens (Optional)**

- Professionals often need to pass arguments, especially in apps with detail/edit screens.

```dart
// Passing data
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => ProfileScreen(user: currentUser)),
);

// Receiving data (in ProfileScreen)
final User user;
ProfileScreen({required this.user});
```

---

## Professional Practice

- **File Organization:** Each screen in its own file under `lib/screens/`.
- **Scaffold Usage:** Wrap every screen widget with `Scaffold` for consistent structure (AppBar, Drawer, FAB).
- **Navigation:** Use named routes for maintainability. For large apps, consider [go_router](https://pub.dev/packages/go_router) or [auto_route](https://pub.dev/packages/auto_route) for scalable navigation.
- **State Management:** For screens that interact with data or backend, professionals use Provider, Riverpod, or Bloc for state management instead of holding state locally.
- **Testing:** Write widget tests for each screen in the `test/` directory.

---

## Extra Notes

- **Screen vs. Widget:** All screens are widgets, but not all widgets are screens. Custom widgets (buttons, cards) live in `lib/widgets/`.
- **MVVM/Clean Architecture:** Professionals separate UI (View), logic (ViewModel/Controller), and data (Model/Repository).
- **Lifecycle:** In Flutter, screen lifecycles are handled via widget lifecycle methods (`initState`, `dispose` for StatefulWidget).

---

## Definitions

- **Screen/Page/Route:** A full-page widget that users navigate to.
- **StatelessWidget:** Widget with no internal state (doesn’t change).
- **StatefulWidget:** Widget with mutable internal state (can change).
- **Scaffold:** Provides basic screen structure (AppBar, body, FAB).
- **Navigator:** Flutter’s API for moving between screens.
- **Named Route:** A string identifier for navigation, useful for deep linking and maintainable code.

---

## What’s Next?

- Learn about navigation patterns (push, pop, named routes, deep linking).
- Study state management for data-driven screens.
- Explore custom widgets and screen composition.
- Practice building screens for login, signup, dashboard, and profile.

---

> **Pro Tip:**  
Always keep screens modular (one file per screen), use Scaffold for structure, and manage navigation through named routes or professional packages for scalability.

---