

### **Widget build(BuildContext context)**

---

### **Constant Part**
```dart
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


  The main method of every widget.  
  - `Widget`: The return type, meaning this method produces a widget for the UI.
  - `build`: The method name, called every time Flutter needs to redraw the widget.
  - `(BuildContext context)`: A parameter that gives information about where the widget is in the widget tree (UI hierarchy).
- **Why Use It:**  
  - `build` is required for all widgets.
  - `context` lets you access theme, navigation, localization, and parent widget data, making your UI flexible and responsive.

---


---

## Extra Notes (Going Beyond)

- **BuildContext:**  
  Can access inherited widgets, themes, navigation, and screen size. Essential for advanced UI work.
- **Widget Tree:**  
  Flutter UIs are structured as nested widgets (the widget tree). `build` constructs this tree.
- **Screen Navigation:**  
  Use `Navigator` or professional packages (e.g., `go_router`) to switch between screens.
- **Testing:**  
  Professionals write widget tests to verify build outputs and UI behavior.

---

## Definitions

- **Class:** A blueprint for creating objects (code structure).
- **Inheritance (extends):** Gaining properties and methods from another class.
- **StatelessWidget:** Widget with no mutable state (doesn’t change).
- **StatefulWidget:** Widget with mutable state (can change).
- **Annotation (@override):** Special marker for compiler checks.
- **BuildContext:** Metadata/context about where the widget lives in the UI tree.
- **Scaffold:** High-level layout widget for full pages/screens.
- **AppBar:** Top bar with title and actions.
- **Center:** Widget that centers its child.
- **Text:** Widget for displaying text.

---
---
