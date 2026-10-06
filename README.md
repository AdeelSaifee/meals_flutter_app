# Meals App — Flutter Multi-Screen Navigation, Riverpod & Animations

A production-ready multi-screen mobile recipe and meal exploration application built with Flutter, Dart, **Riverpod**, and **Flutter Animation Architecture**. The application demonstrates real-world mobile navigation architectures, scalable app-wide reactive state management, and silky smooth explicit, implicit, and multi-screen transitions.

Targeted and optimized strictly for **Android** and **iOS**.

---

## 🍽️ Application Features

- **Category Browsing with Slide-in Animation**: Interactive grid of culinary categories featuring gradient styling, Material splash ripple feedback (`InkWell`), and an explicit bottom-to-top slide transition (`SlideTransition` + `CurvedAnimation`).
- **Meals Exploration**: Filtered list of recipes matching selected categories with duration, complexity, and affordability indicators.
- **Cross-Screen Hero Image Transitions**: Tapping any recipe card triggers a seamless, physics-based flight transition (`Hero` widget with unique `meal.id` tags) expanding the recipe photo directly into the details screen.
- **Interactive Favorite Button Animation**: AppBar favorite star button with an implicit animated spin and swap transition (`AnimatedSwitcher` + `RotationTransition` + `ValueKey`).
- **Dynamic Favorite Meals Management**: Add and remove meals from a personal Favorites list with instantaneous cross-screen synchronization via Riverpod.
- **Dietary Filters & Preferences**: Dynamic dietary filtering based on user preferences (Gluten-Free, Lactose-Free, Vegetarian, Vegan) managed cleanly by `filtersProvider`.
- **Dependent Provider Architecture**: `filteredMealsProvider` combines `mealsProvider` and `filtersProvider` behind the scenes, automatically re-filtering recipes without polluting UI widgets.
- **Multi-Screen Navigation Architecture**:
  - **Hierarchical Stack Navigation**: Pushing and popping screens smoothly using `Navigator.push` and `Navigator.pop`.
  - **Tabs Bar Navigation**: Bottom navigation bar (`BottomNavigationBar`) to toggle smoothly between Categories and Favorites.
  - **Side Drawer Navigation**: Accessible side drawer (`Drawer`) for switching between Meals and Filter settings without stack buildup.
- **Theming & Typography**: Cohesive Material Design 3 system with custom color schemes and typography from Google Fonts.

---

## 🧠 Key Learnings & Flutter Concepts Mastered

### 1. Flutter Animation Architecture (Module 10)
- **Explicit Animations (Fine-Grained Custom Control)**:
  - **`AnimationController`**: Configuring custom durations, tick synchronization, and manual lifecycle triggers (`forward()`, `stop()`, `repeat()`, `dispose()`).
  - **`SingleTickerProviderStateMixin` & `vsync`**: Binding animations directly to device hardware screen refresh rates (60/120 FPS) for battery optimization and tear-free rendering.
  - **`AnimatedBuilder` & The Cached Child Technique**: High-performance rendering pattern where static widgets (`GridView`) are declared in the `child` slot and reused across frames, preventing heavy rebuilds 60 times/sec.
  - **`Tween` & `CurvedAnimation`**: Translating raw controller values (`0.0` to `1.0`) into geometric coordinates (`Offset(0, 0.3)` to `Offset.zero`) using organic deceleration curves (`Curves.easeInOut`).
  - **`SlideTransition`**: Hardware-accelerated position shifting based on `Animation<Offset>`.
- **Implicit Animations (Zero Boilerplate)**:
  - **`AnimatedSwitcher`**: Animating transitions between distinct widgets when states change.
  - **Widget Keys (`ValueKey`)**: Forcing Flutter's element tree to recognize mutations across identical widget types (`Icon` ➔ `Icon`) and trigger implicit switch transitions.
  - **`RotationTransition` with Tweens**: Tuning spin effects (`0.8` to `1.0` turn) for subtle, pleasant UI micro-interactions.
- **Multi-Screen Shared Element Transitions (`Hero` Animations)**:
  - Flying elements across navigation routes (`Navigator.push` / `Navigator.pop`) using shared, unique tags (`tag: meal.id`).
  - Automatic overlay flight geometry calculation and reverse-flight interpolation handled natively by Flutter.

### 2. App-wide State Management with Riverpod (Module 09)
- **Elimination of "Prop Drilling"**: Direct global state access without intermediary parameter passing.
- **`ProviderScope`**: App root wrapper providing dependency injection and state lifecycle management.
- **`Provider` vs. `StateNotifierProvider`**: Clean separation of read-only providers and immutable state notifiers (`state = [...]`, `state = {...}`).
- **`ConsumerWidget` & `ConsumerStatefulWidget`**: Reactive widget tree consumption via `WidgetRef ref`.
- **`ref.watch` vs. `ref.read`**: Subscribing to continuous updates in build methods vs. one-off method dispatch in event callbacks.
- **Dependent Providers**: Declarative state chaining combining multiple providers into a synchronized data pipeline.

### 3. Multi-Screen Navigation Architecture (Module 08)
- Hierarchical stack navigation with `MaterialPageRoute`.
- Tab bar navigation (`BottomNavigationBar`) and slide drawers (`Drawer`).
- Hardware and gesture back interception with modern `PopScope`.

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
│   ├── categories.dart                 # Categories grid with explicit SlideTransition
│   ├── filters.dart                    # Dietary filters screen (Stateless ConsumerWidget)
│   ├── meal_details.dart               # Detailed recipe with Hero image & AnimatedSwitcher
│   ├── meals.dart                      # Filtered meals list screen
│   └── tabs.dart                       # Main navigation scaffold (Bottom tabs & drawer)
└── widgets/
    ├── category_grid_item.dart         # Gradient card for category items
    ├── main_drawer.dart                # Slide-out drawer menu
    ├── meal_item.dart                  # Meal card item with Hero image transition
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
