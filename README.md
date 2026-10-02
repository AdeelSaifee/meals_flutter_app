# Meals App — Flutter Multi-Screen Navigation

A multi-screen mobile recipe and meal exploration application built with Flutter and Dart. The application demonstrates real-world multi-screen mobile architecture: navigating across hierarchical screen stacks, passing data forward and backward, tab bar navigation, side drawer menus, and dynamic cross-screen state management for favorites and dietary filters.

Targeted and optimized strictly for **Android** and **iOS**.

---

## 🍽️ Application Features

- **Category Browsing**: Visual grid of food categories with gradient styling and Material splash touch feedback.
- **Meals Exploration**: Filtered list of recipes belonging to selected categories with duration, complexity, and affordability indicators.
- **Detailed Recipe Screen**: Complete meal instructions, ingredient checklists, and step-by-step preparation guidelines with an AppBar favorite toggle button.
- **Favorite Meals Management**: Add and remove meals from a personal Favorites list with instantaneous cross-screen synchronization.
- **Dietary Filters & Preferences**: Dynamic filtering based on user preferences:
  - Gluten-Free
  - Lactose-Free
  - Vegetarian
  - Vegan
- **Multi-Screen Navigation Patterns**:
  - **Hierarchical Stack Navigation**: Pushing and popping screens smoothly using `Navigator.push` and `Navigator.pop`.
  - **Tabs Bar Navigation**: Bottom navigation bar (`BottomNavigationBar`) to toggle smoothly between Categories and Favorites.
  - **Side Drawer**: Slide-out navigation drawer (`Drawer`) for switching between Meals and Filter settings without stack buildup.
- **Theming & Typography**: Cohesive Material Design 3 system with custom color schemes and typography from Google Fonts.

---

## 🧠 Key Learnings & Flutter Concepts Mastered

### 1. Multi-Screen Navigation & Stack Management
- **`Navigator.push` & `Navigator.pop`**:
  - Managing the navigation stack for pushing recipe lists, meal details, and returning results.
  - Using `MaterialPageRoute` for platform-authentic slide and fade screen transitions.
- **Passing Data Between Screens**:
  - Passing models and category identifiers via widget constructors.
  - Returning data back to previous screens using `Navigator.of(context).pop(data)`.

### 2. Tab Bar & Drawer Architectures
- **Bottom Navigation Bar (`BottomNavigationBar`)**:
  - Setting up persistent tab navigation for high-level screen switching.
  - Managing active screen index and dynamic `AppBar` titles based on the active tab.
- **Side Drawer Navigation (`Drawer`)**:
  - Implementing accessible side drawers with custom headers and `ListTile` options.
  - Replacing or pushing routes cleanly using `Navigator.of(context).pushReplacement` to avoid infinite navigation history loops.

### 3. State Management & Cross-Screen Filtering
- **Lifting State Up & Callbacks**:
  - Managing global favorites and filter toggles at the root level and passing callbacks down the widget tree.
- **Dynamic List Filtering**:
  - Applying functional list filters (`where` and predicate functions) to filter meals based on user toggles.
- **State Preservation**:
  - Preserving user filter choices across screen transitions and navigation drawer switches.

### 4. Interactive UI & Custom Layouts
- **`GridView` & Sliver Delegates**:
  - Building responsive grids using `SliverGridDelegateWithFixedCrossAxisCount` with aspect ratios and spacing.
  - Handling touch feedback using `InkWell` for Material ripple effects.
- **Card-Based Media Representations**:
  - Layering meal thumbnail images, gradient overlays, and metadata labels using `Stack` and `Positioned`.

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
│   ├── categories.dart                 # Categories grid screen
│   ├── filters.dart                    # Dietary preferences filter screen
│   ├── meal_details.dart               # Detailed ingredients & recipe steps
│   ├── meals.dart                      # Filtered meals list screen
│   └── tabs.dart                       # Main navigation scaffold (Bottom tabs & Drawer)
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
