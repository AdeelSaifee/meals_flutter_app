# Meals App — Flutter Multi-Screen Navigation

A multi-screen mobile recipe and meal exploration application built with Flutter and Dart. The application demonstrates real-world mobile navigation architectures: hierarchical screen stacks, bi-directional data flow, bottom navigation tabs, slide-out drawer menus, system back gesture interception with modern `PopScope`, and dynamic cross-screen filter state management.

Targeted and optimized strictly for **Android** and **iOS**.

---

## 🍽️ Application Features

- **Category Browsing**: Interactive grid of culinary categories featuring gradient styling and Material splash ripple feedback (`InkWell`).
- **Meals Exploration**: Filtered list of recipes matching selected categories with duration, complexity, and affordability indicators.
- **Detailed Recipe Screen**: Complete meal instructions, ingredient checklists, and step-by-step preparation guidelines with an AppBar favorite toggle button.
- **Favorite Meals Management**: Add and remove meals from a personal Favorites list with instantaneous cross-screen synchronization.
- **Dietary Filters & Preferences**: Dynamic dietary filtering based on user preferences:
  - Gluten-Free
  - Lactose-Free
  - Vegetarian
  - Vegan
- **Persistent In-Session Filter State**: Filters set in the `FiltersScreen` are saved into `TabsScreen` and automatically restored via `initState` whenever the filters screen is reopened.
- **Dynamic Category Filtering**: Categories screen only presents meals that pass the currently active dietary filter conditions (`availableMeals`), while keeping favorite meals unhindered.
- **Multi-Screen Navigation Architecture**:
  - **Hierarchical Stack Navigation**: Pushing and popping screens smoothly using `Navigator.push` and `Navigator.pop`.
  - **Two-Way Data Passing**: Awaiting data from pushed routes (`Future<Map<Filter, bool>>`) and returning maps via `Navigator.pop(result)`.
  - **Hardware Back Navigation Interception**: Leveraging modern Flutter (3.22+) `PopScope` (`canPop: false`, `onPopInvokedWithResult`) to guarantee filters return to parent screen regardless of how the user navigates back.
  - **Tabs Bar Navigation**: Bottom navigation bar (`BottomNavigationBar`) to toggle smoothly between Categories and Favorites.
  - **Side Drawer Navigation**: Accessible side drawer (`Drawer`) for switching between Meals and Filter settings without stack buildup.
- **Theming & Typography**: Cohesive Material Design 3 system with custom color schemes and typography from Google Fonts.

---

## 🧠 Key Learnings & Flutter Concepts Mastered

### 1. Multi-Screen Navigation & Stack Management
- **`Navigator.push` & `Navigator.pop`**:
  - Managing the navigation stack for pushing recipe lists, meal details, and returning results.
  - Using `MaterialPageRoute` for platform-authentic slide and fade screen transitions with complete compile-time type safety.
- **Bi-Directional Data Transfer**:
  - Passing models and category identifiers forward via widget constructors.
  - Returning data back to previous screens using `Navigator.of(context).pop(data)` and consuming it via `await Navigator.of(context).push<T>(...)`.
- **Interception with `PopScope`**:
  - Controlling back navigation and returning data consistently across both AppBar back buttons and Android hardware/gesture back events.

### 2. Tab Bar & Drawer Architectures
- **Bottom Navigation Bar (`BottomNavigationBar`)**:
  - Setting up persistent tab navigation for high-level screen switching.
  - Managing active screen index and dynamic `AppBar` titles based on the active tab.
- **Side Drawer Navigation (`Drawer`)**:
  - Implementing accessible side drawers with custom headers and `ListTile` options.
  - Replacing or pushing routes cleanly to manage screen hierarchy without unnecessary stack buildup.

### 3. State Management & Dynamic List Filtering
- **Lifting State Up & Callbacks**:
  - Managing global favorites and filter toggles at the root level (`TabsScreen`) and passing callbacks down the widget tree.
- **Functional List Filtering**:
  - Applying functional list filters (`where` and predicate functions) to filter dummy meals based on active user toggles.
- **State Preservation via Lifecycle Hooks**:
  - Passing active filters back into `FiltersScreen` and restoring local switch states inside `initState()` using `widget.currentFilters`.

### 4. Navigation Paradigms Evaluated
- **Direct `MaterialPageRoute` (Course Approach)**:
  - Strong compile-time type safety, zero external dependencies, native platform transitions, and explicit constructor contracts.
- **Named Routes (`pushNamed`)**:
  - Understanding string-based routing trade-offs, lack of compile-time checking, and argument casting limitations.
- **Modern Routing Packages (`go_router`)**:
  - Exploring declarative navigation, URL syncing, deep linking, and web application routing architectures.

---

## 📁 Project Structure

```text
lib/
├── main.dart                           # Entry point, theme configuration, & root widget
├── data/
│   └── dummy_data.dart                 # Mock data sets for categories and meals
├── models/
│   ├── category.dart                   # Category data model
│   └── meal.dart                       # Meal model with enums (Complexity, Affordability)
├── screens/
│   ├── categories.dart                 # Categories grid screen (consumes availableMeals)
│   ├── filters.dart                    # Dietary preferences filter screen (PopScope & initState)
│   ├── meal_details.dart               # Detailed ingredients & recipe steps
│   ├── meals.dart                      # Filtered meals list screen
│   └── tabs.dart                       # Main navigation scaffold (Bottom tabs, Drawer, Filter state)
└── widgets/
    ├── category_grid_item.dart         # Gradient card for category items
    ├── main_drawer.dart                # Slide-out drawer menu
    ├── meal_item.dart                  # Meal card item with image & metadata
    └── meal_item_trait.dart            # Icon + label metadata badge
```

---

## 🚀 Getting Started

### Prerequisites
- Flutter SDK (v3.16.0 or higher recommended)
- Android Studio / Xcode for emulators and physical device deployment

### Dependencies
Defined in `pubspec.yaml`:
- `google_fonts`: Dynamic typography
- `transparent_image`: Smooth image fade-in placeholders

### Running the App
1. Clone the repository:
   ```bash
   git clone https://github.com/AdeelSaifee/meals_flutter_app.git
   cd meals_flutter_app
   ```

2. Fetch dependencies:
   ```bash
   flutter pub get
   ```

3. Run static code analysis:
   ```bash
   flutter analyze
   ```

4. Launch the application:
   ```bash
   flutter run
   ```
