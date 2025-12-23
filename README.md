# Product Catalog App

A React Native mobile application for browsing and managing products. Users can explore products, search by category or keyword, view detailed product information, and maintain a wishlist of their favorite items.

## App Functionality

Here's what the app does:

- **Welcome Screen**: A landing screen that introduces users to the app
- **Home Tab**: Displays all available products in a 2-column grid layout with images, titles, and prices. Includes infinite scroll pagination to load more products as you scroll.
- **Search Tab**: 
  - Shows product categories in a 2-column grid when first opened
  - Allows users to search for products by entering keywords in the search bar
  - Displays search results in a product grid with infinite scroll pagination
- **Wishlist Tab**: 
  - Shows all saved products
  - Allows users to add/remove products from wishlist
  - Persists wishlist data across app restarts
- **Product Details Screen**: 
  - Displays comprehensive product information including images, title, brand, price, discount, rating, and description
  - Shows product metadata (category, stock, availability, shipping, warranty)
  - Displays customer reviews
  - Allows users to add/remove products from wishlist
- **Category Screen**: Shows all products filtered by a specific category with infinite scroll pagination for efficient loading

The app fetches product data from the [DummyJSON API](https://dummyjson.com) to provide a smooth, native mobile experience for browsing and managing products. All API calls are handled through a centralized service layer with support for pagination, search, and category filtering.

## How to Run the Project

**APK build:** [Download here](https://drive.google.com/file/d/1Ye5HDFdSKE1-v81v5xsaQD9lh6WCqmeu/view?usp=sharing)

### Prerequisites

Before running the project, ensure you have the following installed:

- **Node.js** (version >= 20) - [Download Node.js](https://nodejs.org/)
- **React Native CLI** - Use `npx` (recommended) or install globally with `npm install -g react-native-cli`
- **React Native development environment** - Follow the [official setup guide](https://reactnative.dev/docs/set-up-your-environment)

**Project Versions:**
- React Native 0.83.1
- React 19.2.0
- TypeScript 5.8.3

**For Android development:**
- Android Studio with Android SDK
- Android SDK Platform (compileSdkVersion 36, minSdkVersion 24)
- Android Virtual Device (AVD) or a physical Android device with USB debugging enabled

**For iOS development (macOS only):**
- Xcode (latest version recommended)
- CocoaPods - Install with `sudo gem install cocoapods`
- iOS Simulator or a physical iOS device

### Installation Steps

1. **Clone or navigate to the project directory:**
```sh
cd test-assignment
```

2. **Install dependencies:**
```sh
npm install
# OR
yarn install
```

**Note:** This project uses React Native CLI (not Expo). Make sure you have completed the React Native development environment setup before proceeding.

3. **Install iOS dependencies (macOS only):**
```sh
cd ios
pod install
cd ..
```

### Running the App

#### Run on Android

1) Start Metro (bundler):

```sh
npm start
# OR
yarn start
# OR
npx react-native start
```

Keep this terminal open.

2) In a new terminal, run:

```sh
npx react-native run-android
```

This will build the Android app, launch the emulator (if configured) or install on a connected device, and connect to Metro automatically.

**Note:** Ensure an emulator is running or a USB device with debugging enabled is connected.

#### Run on iOS (macOS only)

1) Start Metro (bundler) as above, then in a new terminal run:

```sh
npx react-native run-ios
```

This will build the iOS app, launch the iOS Simulator, and connect to Metro automatically. The first run may take several minutes as Xcode builds the app.

### Development Tips

- **Fast Refresh**: Enabled by default - changes to your code will automatically reload in the app
- **Manual Reload**: 
  - **Android**: Press <kbd>R</kbd> twice or shake device and select "Reload"
  - **iOS**: Press <kbd>Cmd ⌘</kbd> + <kbd>R</kbd> in Simulator or shake device
- **Dev Menu**: 
  - **Android**: Press <kbd>Ctrl</kbd> + <kbd>M</kbd> (Windows/Linux) or <kbd>Cmd ⌘</kbd> + <kbd>M</kbd> (macOS) in emulator, or shake device
  - **iOS**: Press <kbd>Cmd ⌘</kbd> + <kbd>D</kbd> in Simulator or shake device
- **Debugging**: Use React Native Debugger or Chrome DevTools (accessible from Dev Menu)

### Troubleshooting

**Metro bundler issues:**
- Clear Metro cache: `npm start -- --reset-cache`
- Clear watchman: `watchman watch-del-all`

**Android build issues:**
- Ensure Android SDK is properly configured
- Check that ANDROID_HOME environment variable is set
- Try cleaning the build: `cd android && ./gradlew clean && cd ..`

**iOS build issues:**
- Run `pod install` again in the `ios` directory
- Clean build folder in Xcode: Product → Clean Build Folder
- Delete `ios/build` folder and rebuild

**Dependencies issues:**
- Delete `node_modules` and `package-lock.json`/`yarn.lock`, then run `npm install` again
- For iOS, delete `ios/Pods` and `Podfile.lock`, then run `pod install` again

## Technologies & Dependencies

### Core
- **React Native** 0.83.1 - Mobile framework
- **React** 19.2.0 - UI library
- **TypeScript** 5.8.3 - Type safety

### Navigation
- **@react-navigation/native** 7.1.26 - Navigation library
- **@react-navigation/native-stack** 7.9.0 - Stack navigator
- **@react-navigation/bottom-tabs** 7.9.0 - Tab navigator
- **react-native-screens** 4.19.0 - Native screen components
- **react-native-safe-area-context** 5.6.2 - Safe area handling

### State Management
- **@reduxjs/toolkit** 2.11.2 - Redux state management
- **react-redux** 9.2.0 - React bindings for Redux
- **redux-persist** 6.0.0 - State persistence
- **@react-native-async-storage/async-storage** 2.2.0 - Async storage for persistence

### Networking
- **axios** 1.13.2 - HTTP client for API calls

### UI Components
- **react-native-vector-icons** 10.3.0 - Icon library (Ionicons)

## Key Technical Decisions

1. **React Native with TypeScript**: TypeScript is used to provide type safety throughout the application. This helps catch bugs at compile time rather than runtime, especially when working with API responses and navigation parameters. The type system makes the codebase more maintainable and reduces the likelihood of errors when refactoring or adding new features.

2. **Redux Toolkit with Redux Persist**: 
   - Redux Toolkit (v2.11.2) simplifies state management by reducing boilerplate code and providing built-in best practices
   - Redux Persist (v6.0.0) with AsyncStorage (@react-native-async-storage/async-storage v2.2.0) ensures the wishlist data persists across app restarts, providing a better user experience where users don't lose their saved items
   - Wishlist slice includes actions: `addToWishlist`, `removeFromWishlist`, and `toggleWishlist` for flexible wishlist management
   - Only essential product data (id, title, price, images) is stored in the wishlist to optimize storage usage

3. **React Navigation (Static Navigation v7)**:
   - The static navigation configuration from React Navigation v7 (@react-navigation/native v7.1.26, @react-navigation/native-stack v7.9.0, @react-navigation/bottom-tabs v7.9.0) provides type-safe navigation, catching navigation errors at compile time
   - Combining Stack Navigator (Welcome, Tab, Details, Category screens) and Tab Navigator (Home, Search, Wishlist tabs) creates a native app feel with smooth transitions
   - Navigation structure: Welcome → Tab Navigator → (Home/Search/Wishlist) with Details and Category as stack screens
   - Type-safe navigation prevents runtime errors from incorrect route names or missing parameters

4. **Axios for API Calls**:
   - A centralized API service layer using Axios (v1.13.2) keeps all API logic organized in one place, making it easier to maintain and update
   - The class-based structure (`ProductsApi`) provides a clean interface with methods for fetching products, categories, search, and pagination
   - Configuring the base URL (https://dummyjson.com) centrally makes it simple to swap out the backend API or switch between development and production environments
   - Supports pagination parameters (limit, skip) for efficient data loading

5. **Component Architecture**:
   - Reusable components (ProductCard, SearchListComponent, CategoryComponent, ReviewComponent) follow the DRY principle, reducing code duplication
   - ProductCard is used consistently across Home, Search, and Category screens for a unified UI experience
   - Each screen manages its own state and API calls, keeping concerns separated and making the code easier to understand and maintain
   - This component separation enables easy reuse across different screens and simplifies testing

6. **Safe Area Context**: The `react-native-safe-area-context` library properly handles device-specific safe areas (notches, status bars) across different devices. This ensures the app's UI is correctly positioned on all devices, especially newer iPhones with notches, preventing content from being obscured by system UI elements.

7. **React Native Vector Icons**: Ionicons (react-native-vector-icons v10.3.0) are used for tab bar icons because they're well-maintained, scalable, and provide a consistent visual design across the app. Vector icons scale perfectly at any size and maintain crisp quality on all screen densities. Icons used: home/home-outline, search/search-outline, heart/heart-outline with a custom active color (#E53935).

8. **Pagination Implementation**: Infinite scroll pagination is implemented on Home, Search, and Category screens using FlatList's `onEndReached` callback. Products are loaded in batches of 20 items, reducing initial load time and memory usage. Loading indicators are shown at the bottom of lists when fetching more data.

## Project Structure

```
testing/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── CategoryComponent.tsx
│   │   ├── ProductCard.tsx
│   │   ├── ReviewComponent.tsx
│   │   ├── SearchListComponent.tsx
│   │   └── index.ts
│   ├── screens/             # Screen components
│   │   ├── tabs/           # Tab navigator screens
│   │   │   ├── HomeScreen.tsx
│   │   │   ├── SearchScreen.tsx
│   │   │   └── Wishlist.tsx
│   │   ├── Category.tsx
│   │   ├── ProductDetails.tsx
│   │   ├── Welcome.tsx
│   │   └── index.ts
│   ├── navigation/          # Navigation configuration
│   │   ├── StackNavigator.tsx
│   │   └── TabNavigator.tsx
│   ├── styles/             # StyleSheet definitions
│   └── constants/          # Constants and utilities
├── services/               # API service layer
│   ├── products/
│   │   ├── index.ts       # ProductsApi class
│   │   └── types.ts       # TypeScript interfaces
│   └── index.ts           # Main API instance
├── store/                  # Redux store configuration
│   ├── index.ts
│   └── WishlistSlice.ts
├── android/                # Android native code
├── ios/                    # iOS native code
└── App.tsx                 # Root component
```

## Improvements with More Time

With additional development time, the following improvements would enhance the app's functionality, performance, and user experience:

1. **Better Error Handling & User Feedback**:
   - Currently, errors are primarily logged to the console. Error boundaries would catch React errors gracefully and display user-friendly error screens
   - Toast notifications (using libraries like `react-native-toast-message`) would provide immediate feedback for user actions like adding items to wishlist or handling search failures
   - For API failures, retry buttons and more descriptive error messages would improve the user experience instead of generic "Failed to load" messages

2. **Performance Optimizations**:
   - Product images reload on every screen visit, which impacts performance. Image caching using `react-native-fast-image` or similar libraries would significantly improve load times and reduce bandwidth usage
   - Infinite scroll pagination is already implemented on Home, Search, and Category screens. Additional optimizations like virtualization tuning and loading states could enhance the experience
   - Optimizing FlatList components with `React.memo` and proper key extraction would reduce unnecessary re-renders and improve scrolling performance

3. **Enhanced Features**:
   - Adding filtering and sorting options (by price, rating, popularity, etc.) would make product browsing more efficient and user-friendly
   - A shopping cart feature would enable users to collect multiple items before making a purchase decision
   - User authentication would unlock personalized features like saved searches, purchase history, and product recommendations
   - A product comparison feature would help users make informed decisions when choosing between similar items

4. **Testing**:
   - Unit tests for Redux slices (especially wishlist logic) and API services would ensure business logic works correctly and prevent regressions
   - Integration tests for navigation flows would verify that the app's navigation works as expected across different user journeys
   - Component tests using React Native Testing Library would validate that UI components render correctly and handle user interactions properly

5. **UI/UX Polish**:
   - Replacing basic "Loading..." text with skeleton loaders that match the actual content layout would provide better visual feedback during data fetching
   - Pull-to-refresh functionality would make the app feel more responsive and give users control over data updates
   - Smooth animations and transitions would enhance the perceived performance and make navigation feel more polished
   - Improved empty states with helpful illustrations or actionable suggestions would guide users when no data is available

6. **Code Quality & Developer Experience**:
   - ESLint and Prettier configurations would enforce consistent code style across the codebase, making it easier for multiple developers to work on the project
   - Enabling TypeScript strict mode would catch additional type-related issues at compile time, improving code reliability
   - JSDoc comments would improve code documentation and make the codebase more maintainable for future developers
   - A CI/CD pipeline would automate testing and deployment processes, reducing manual errors and speeding up the development cycle

7. **Offline Support**:
   - Caching product data locally would allow users to browse previously viewed products even without an internet connection
   - Implementing a sync mechanism when the connection is restored would ensure data consistency between local cache and server
   - This would significantly improve app reliability in areas with poor or intermittent connectivity

8. **Accessibility**:
   - Proper accessibility labels and hints would enable screen readers to navigate the app, making it usable for visually impaired users
   - Ensuring proper contrast ratios would improve readability for users with visual impairments
   - These improvements would make the app more inclusive and accessible to a wider range of users
