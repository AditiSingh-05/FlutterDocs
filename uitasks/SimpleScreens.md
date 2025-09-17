# README 8: Professional Guide — Building Modern Flutter Banking UIs (3 Screens)

---

## Introduction

This guide walks you through creating three modern, professional banking app screens in Flutter, inspired by the UI in ![image1](image1):  
1. **Dashboard/Home** (Balance, Cards, Transactions)  
2. **Add Money** (Card selection, deposit options)  
3. **Profile** (Personal info, account info)  

You’ll learn how to break down complex UIs into Flutter widgets, organize files, handle layouts, apply decoration, and build scalable, maintainable code — everything a professional developer would do.

---

## 1. Project Structure and Preparation

### **Industry Standard Folder Structure**

```
lib/
  main.dart
  screens/
    dashboard_screen.dart
    add_money_screen.dart
    profile_screen.dart
  widgets/
    card_widget.dart
    transaction_tile.dart
    info_section.dart
  models/
    user.dart
    card.dart
    transaction.dart
  assets/
    images/
      debit_card.png
      credit_card.png
      user_avatar.png
```

**Professional Practice:**  
- Each screen in its own Dart file.
- Reusable UI pieces (custom cards, tiles) in `widgets/`.
- Data models in `models/`.
- All static images in `assets/images/`.

Register assets in `pubspec.yaml`:
```yaml
flutter:
  assets:
    - assets/images/
```

---

## 2. Dashboard/Home Screen — UI Breakdown

### **Key Components**

- Top greeting, balance, toggle visibility, add money button
- Horizontal card carousel ("Your cards")
- Transactions list
- Bottom navigation bar

### **Step-by-Step Implementation**

**Scaffold Structure:**
```dart
Scaffold(
  backgroundColor: Color(0xFFF7F8FA),
  appBar: PreferredSize(
    preferredSize: Size.fromHeight(70),
    child: Padding(
      padding: EdgeInsets.all(16),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text('Good morning, Terry', style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
              Text('Welcome to Neobank', style: TextStyle(color: Colors.grey)),
            ],
          ),
          Icon(Icons.notifications_none, size: 28),
        ],
      ),
    ),
  ),
  body: SingleChildScrollView(
    child: Column(
      children: [
        // Balance card
        Container(
          margin: EdgeInsets.all(16),
          padding: EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(20),
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text('Your balance', style: TextStyle(color: Colors.grey)),
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  Text('\$3,200.00', style: TextStyle(fontSize: 32, fontWeight: FontWeight.bold)),
                  Icon(Icons.visibility_off_outlined),
                ],
              ),
              SizedBox(height: 12),
              ElevatedButton(
                onPressed: () {},
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.black,
                  shape: StadiumBorder(),
                  padding: EdgeInsets.symmetric(vertical: 16),
                ),
                child: Text('Add money', style: TextStyle(fontSize: 16)),
              ),
            ],
          ),
        ),
        // Cards carousel (ListView.horizontal)
        Padding(
          padding: EdgeInsets.symmetric(horizontal: 16),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Text('Your cards', style: TextStyle(fontWeight: FontWeight.bold)),
              Text('+ New card', style: TextStyle(color: Colors.green)),
            ],
          ),
        ),
        Container(
          height: 160,
          margin: EdgeInsets.symmetric(vertical: 10),
          child: ListView(
            scrollDirection: Axis.horizontal,
            children: [
              CardWidget(...), // custom card widget
              CardWidget(...),
              // more cards
            ],
          ),
        ),
        // Transactions
        Padding(
          padding: EdgeInsets.symmetric(horizontal: 16),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Text('Transactions', style: TextStyle(fontWeight: FontWeight.bold)),
              Text('See all', style: TextStyle(color: Colors.green)),
            ],
          ),
        ),
        ListView.builder(
          shrinkWrap: true,
          physics: NeverScrollableScrollPhysics(),
          itemCount: transactions.length,
          itemBuilder: (context, index) => TransactionTile(transaction: transactions[index]),
        ),
      ],
    ),
  ),
  bottomNavigationBar: NavigationBar(
    destinations: [
      NavigationDestination(icon: Icon(Icons.home), label: 'Home'),
      NavigationDestination(icon: Icon(Icons.map), label: 'Map'),
      NavigationDestination(icon: Icon(Icons.swap_horiz), label: 'Transfer'),
      NavigationDestination(icon: Icon(Icons.settings), label: 'Settings'),
      NavigationDestination(icon: CircleAvatar(...), label: 'Profile'),
    ],
  ),
)
```

**Professional Enhancements:**  
- Use data models for cards and transactions.
- Use custom widgets for cards and transaction tiles.
- Apply theme and color palette consistently.

---

## 3. Add Money Screen — UI Breakdown

### **Key Components**

- Top bar with back arrow and title
- Horizontal card selector
- Action list (move deposit, transfer, Apple Pay, debit/credit card)

### **Step-by-Step Implementation**

**Scaffold Structure:**
```dart
Scaffold(
  backgroundColor: Color(0xFFF7F8FA),
  appBar: AppBar(
    backgroundColor: Colors.transparent,
    elevation: 0,
    leading: IconButton(icon: Icon(Icons.arrow_back), onPressed: () {}),
    title: Text('Add money', style: TextStyle(color: Colors.black)),
    centerTitle: true,
  ),
  body: Padding(
    padding: EdgeInsets.all(16),
    child: Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text('Select card', style: TextStyle(fontWeight: FontWeight.bold)),
        SizedBox(height: 12),
        Container(
          height: 90,
          child: ListView(
            scrollDirection: Axis.horizontal,
            children: [
              CardWidget(...), // show different cards
              CardWidget(...),
            ],
          ),
        ),
        SizedBox(height: 24),
        Text('Add money to Neobank', style: TextStyle(fontWeight: FontWeight.bold)),
        SizedBox(height: 8),
        InfoSection(
          icon: Icons.account_balance_wallet,
          label: 'Move your direct deposit',
          onTap: () {},
        ),
        InfoSection(
          icon: Icons.swap_horiz,
          label: 'Transfer from other banks',
          onTap: () {},
        ),
        InfoSection(
          icon: Icons.phone_iphone,
          label: 'Apple Pay',
          onTap: () {},
        ),
        InfoSection(
          icon: Icons.credit_card,
          label: 'Debit / Credit Card',
          onTap: () {},
        ),
      ],
    ),
  ),
)
```

**Professional Enhancements:**  
- Use models to represent cards and actions.
- Use custom widgets (`InfoSection`) for consistency and reusability.
- Add tap feedback and navigation.

---

## 4. Profile Screen — UI Breakdown

### **Key Components**

- Top bar with profile picture and edit icon
- Personal info section (name, email, phone, address, edit button)
- Account info section

### **Step-by-Step Implementation**

**Scaffold Structure:**
```dart
Scaffold(
  backgroundColor: Color(0xFFF7F8FA),
  appBar: AppBar(
    backgroundColor: Colors.transparent,
    elevation: 0,
    title: Text('Profile', style: TextStyle(color: Colors.black)),
    centerTitle: true,
  ),
  body: SingleChildScrollView(
    padding: EdgeInsets.all(16),
    child: Column(
      children: [
        // Profile avatar
        CircleAvatar(
          radius: 44,
          backgroundImage: AssetImage('assets/images/user_avatar.png'),
        ),
        SizedBox(height: 8),
        IconButton(icon: Icon(Icons.edit), onPressed: () {}),
        SizedBox(height: 24),
        // Personal Info Card
        Container(
          padding: EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(20),
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  Text('Personal info', style: TextStyle(fontWeight: FontWeight.bold)),
                  TextButton(onPressed: () {}, child: Text('Edit')),
                ],
              ),
              Divider(),
              ListTile(
                leading: Icon(Icons.person),
                title: Text('Terry Melton'),
              ),
              ListTile(
                leading: Icon(Icons.email),
                title: Text('melton89@gmail.com'),
              ),
              ListTile(
                leading: Icon(Icons.phone),
                title: Text('+1 201 555-0123'),
              ),
              ListTile(
                leading: Icon(Icons.home),
                title: Text('70 Rainey Street, Apartment 146, Austin TX 78701'),
              ),
            ],
          ),
        ),
        SizedBox(height: 24),
        // Account Info Card
        Container(
          padding: EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(20),
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Text('Account info', style: TextStyle(fontWeight: FontWeight.bold)),
              Divider(),
              // Add account details here
            ],
          ),
        ),
      ],
    ),
  ),
  bottomNavigationBar: NavigationBar(
    destinations: [
      NavigationDestination(icon: Icon(Icons.home), label: 'Home'),
      NavigationDestination(icon: Icon(Icons.map), label: 'Map'),
      NavigationDestination(icon: Icon(Icons.swap_horiz), label: 'Transfer'),
      NavigationDestination(icon: Icon(Icons.settings), label: 'Settings'),
      NavigationDestination(icon: CircleAvatar(...), label: 'Profile'),
    ],
  ),
)
```

**Professional Enhancements:**  
- Use models for user/account info.
- Make “Edit” actions open forms or dialogs (with validation).
- Use custom widgets for info cards.

---

## 5. Professional Practices & Real-World Tips

- **Widget Composition:** Build each UI section as a custom widget, not inline — enables code reuse and clean code.
- **State Management:** For dynamic data (balance, cards, profile info), use Provider, Riverpod, or Bloc.
- **Theming:** Define colors, font sizes, and paddings in a central theme for consistency.
- **Responsiveness:** Use MediaQuery and LayoutBuilder for adaptive designs.
- **Navigation:** Use named routes or go_router for scalable navigation.
- **Accessibility:** Use semantic labels, proper contrast, and large tap targets.

---

## 6. Related Concepts & Next Steps

- **Form Validation:** For editing profile/account info.
- **Network Integration:** Fetch cards, transactions, and profile from backend APIs.
- **MVVM Architecture:** Separate UI, state, and business logic.
- **Testing:** Write widget and integration tests for reliability.
- **Animation:** Add transitions for card selection and navigation.

---

## Definitions

- **Scaffold:** High-level Flutter widget providing app structure (app bar, body, navigation bar).
- **Widget Composition:** Building complex UIs by combining reusable small widgets.
- **ListView:** Scrollable list of widgets, supports horizontal scrolling for carousels.
- **Provider/Riverpod/Bloc:** State management libraries for scalable Flutter apps.
- **ThemeData:** Centralized color, font, and style configuration.
- **MVVM:** Model-View-ViewModel architecture for separation of concerns.

---

## Conclusion

By breaking down each screen into professional Flutter widgets, using custom components, centralizing styles, and following best practices, you can confidently build modern, production-quality UIs like the ones in ![image1](image1).  
Practice building, refactoring, and enhancing these screens — then connect them to real data and navigation for a full app experience.

---

> **Next Steps:**  
Try implementing the above in your project, starting with the Dashboard screen. Experiment with custom widgets, state management, and theming. Once comfortable, move to backend integrations and user authentication for real-world banking apps.

---
