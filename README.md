# Meals App — Flutter Multi-Screen Navigation & Riverpod State Management

A multi-screen mobile recipe and meal exploration application built with Flutter, Dart, and **Riverpod**. The application demonstrates real-world mobile navigation architectures coupled with scalable app-wide reactive state management: eliminating prop drilling, managing cross-widget state, combining local & global state, and orchestrating dependent providers.

Targeted and optimized strictly for **Android** and **iOS**.

---

## 🍽️ Application Features

- **Category Browsing**: Interactive grid of culinary categories featuring gradient styling and Material splash ripple feedback (`InkWell`).
- **Meals Exploration**: Filtered list of recipes matching selected categories with duration, complexity, and affordability indicators.
- **Detailed Recipe Screen**: Complete meal instructions, ingredient checklists, step-by-step preparation guidelines, and an interactive AppBar favorite star toggle button.
- **Dynamic Favorite Meals Management**: Add and remove meals from a personal Favorites list with instantaneous cross-screen synchronization and visual star button swap (`Icons.star` ⟷ `Icons.star_border`).
- **Dietary Filters & Preferences**: Dynamic dietary filtering based on user preferences:
  - Gluten-Free
  - Lactose-Free
  - Vegetarian
  - Vegan
- **Outsourced Filter State (Riverpod)**: Filters managed completely by `filtersProvider`, allowing `FiltersScreen` to be a clean, stateless `ConsumerWidget`.
- **Dependent Provider Architecture**: `filteredMealsProvider` combines `mealsProvider` and `filtersProvider` behind the scenes, automatically re-filtering recipes without polluting UI widgets.
- **Multi-Screen Navigation Architecture**:
  - **Hierarchical Stack Navigation**: Pushing and popping screens smoothly using `Navigator.push` and `Navigator.pop`.
  - **Tabs Bar Navigation**: Bottom navigation bar (`BottomNavigationBar`) to toggle smoothly between Categories and Favorites.
  - **Side Drawer Navigation**: Accessible side drawer (`Drawer`) for switching between Meals and Filter settings without stack buildup.
- **Theming & Typography**: Cohesive Material Design 3 system with custom color schemes and typography from Google Fonts.

---

## 🧠 Key Learnings & Flutter Concepts Mastered

### 1. App-wide State Management with Riverpod (Module 09)
- **Elimination of "Prop Drilling"**:
  - Previously, callbacks (`onToggleFavorite`) and data had to be passed through 4 layers of widgets (`TabsScreen` ➔ `MealsScreen` ➔ `MealItem` ➔ `MealDetailsScreen`).
  - Riverpod allows any widget to directly interact with global state without intermediary parameter passing.
- **`ProviderScope`**:
  - Wrapped around the root widget in `main.dart` to establish the global state store for the entire widget tree.
- **Simple Providers vs. StateNotifierProvider**:
  - **`Provider`**: For immutable or calculated data (`mealsProvider`, `filteredMealsProvider`).
  - **`StateNotifier` & `StateNotifierProvider`**: For mutable, reactive state (`favoriteMealsProvider`, `filtersProvider`) enforcing immutability (`state = [...state]`, `state = {...state}`).
- **`ConsumerWidget` & `ConsumerStatefulWidget`**:
  - Stateless widgets consume providers via `WidgetRef ref` in the `build()` method.
  - Stateful widgets consume providers via `ConsumerState` where `ref` is accessible globally across all lifecycle methods.
- **`ref.watch` vs. `ref.read`**:
  - **`ref.watch`**: Subscribes to provider state changes and triggers widget rebuilds (ideal for `build()` methods).
  - **`ref.read`**: Reads data once or reaches into `.notifier` without subscribing to changes (ideal for callbacks like `onPressed` or `initState`).
- **Dependent Providers (Chaining)**:
  - Providers that consume other providers using `ref.watch` inside their provider declaration function, establishing an automatic reactive dependency graph.

### 2. Multi-Screen Navigation & Stack Management
- **`Navigator.push` & `Navigator.pop`**:
  - Managing the navigation stack for pushing recipe lists, meal details, and filter settings.
  - Using `MaterialPageRoute` for platform-authentic slide and fade screen transitions with complete compile-time type safety.
- **Tab Bar & Drawer Architectures**:
  - Bottom navigation bar (`BottomNavigationBar`) for top-level screen switching.
  - Side drawer (`MainDrawer`) with clean route management.

---

## 📁 Project Structure

```text
lib/
├── main.dart                           # Entry point wrapped in ProviderScope & theme config
├── data/
│   └── dummy_data.dart                 # Mock data sets for categories and meals
├── models/
│   ├── category.dart                   # Category data model
│   └── meal.dart                       # Meal model with enums (Complexity, Affordability)
├── providers/
│   ├── favorites_provider.dart         # favoriteMealsProvider (StateNotifierProvider)
│   ├── filters_provider.dart           # filtersProvider & filteredMealsProvider (Dependent)
│   └── meals_provider.dart             # mealsProvider (Simple Provider)
├── screens/
│   ├── categories.dart                 # Categories grid screen (consumes availableMeals)
│   ├── filters.dart                    # Dietary filters screen (Stateless ConsumerWidget)
│   ├── meal_details.dart               # Detailed recipe with dynamic favorite star button
│   ├── meals.dart                      # Filtered meals list screen
│   └── tabs.dart                       # Main navigation scaffold (Bottom tabs & drawer)
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
- `flutter_riverpod`: State management solution
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
