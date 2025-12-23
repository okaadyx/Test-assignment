# Product Catalog App

A React Native mobile application for browsing and managing products. Users can explore products, search by category or keyword, view detailed product information, and maintain a wishlist of their favorite items.

## App Functionality

Here's what the app does:

- **Welcome Screen**: A landing screen that introduces users to the app
- **Home Tab**: Displays all available products in a grid layout with images, titles, and prices
- **Search Tab**: 
  - Shows product categories in a grid when first opened
  - Allows users to search for products by entering keywords
  - Displays search results in a product grid
- **Wishlist Tab**: 
  - Shows all saved products
  - Allows users to add/remove products from wishlist
  - Persists wishlist data across app restarts
- **Product Details Screen**: 
  - Displays comprehensive product information including images, title, brand, price, discount, rating, and description
  - Shows product metadata (category, stock, availability, shipping, warranty)
  - Displays customer reviews
  - Allows users to add/remove products from wishlist
- **Category Screen**: Shows all products filtered by a specific category

The app fetches product data from the [DummyJSON API](https://dummyjson.com) to provide a smooth, native mobile experience for browsing and managing products.

## How to Run the Project

### Prerequisites

Before running the project, ensure you have the following installed:

- **Node.js** (version >=20) - [Download Node.js](https://nodejs.org/)
- **React Native CLI** - Install globally with `npm install -g react-native-cli` or use npx
- **React Native development environment** - Follow the [official setup guide](https://reactnative.dev/docs/set-up-your-environment)

**For Android development:**
- Android Studio with Android SDK
- Android SDK Platform 33 or higher
- Android Virtual Device (AVD) or a physical Android device with USB debugging enabled

**For iOS development (macOS only):**
- Xcode (latest version recommended)
- CocoaPods - Install with `sudo gem install cocoapods`
- iOS Simulator or a physical iOS device

### Installation Steps

1. **Clone or navigate to the project directory:**
```sh
cd testing
```

2. **Install JavaScript dependencies:**
```sh
npm install
# OR
yarn install
```

3. **Install iOS dependencies (macOS only):**
```sh
cd ios
pod install
cd ..
```

### Running the App

#### Step 1: Start Metro Bundler

Metro is the JavaScript bundler for React Native. Start it in a terminal:

```sh
npm start
# OR
yarn start
```

This will start the Metro bundler and display a QR code. Keep this terminal window open.

#### Step 2: Run on Android

Open a **new terminal window** and run:

```sh
npm run android
# OR
yarn android
```

This will:
- Build the Android app
- Launch the Android Emulator (if configured) or install on a connected device
- Connect to the Metro bundler automatically

**Note:** Make sure you have an Android emulator running or a device connected via USB with USB debugging enabled.

#### Step 2: Run on iOS (macOS only)

Open a **new terminal window** and run:

```sh
npm run ios
# OR
yarn ios
```

This will:
- Build the iOS app
- Launch the iOS Simulator
- Connect to the Metro bundler automatically

**Note:** For the first run, this may take several minutes as Xcode builds the app.

### Alternative: Running with Expo Go (if applicable)

If the project is configured for Expo, you can also run:

```sh
npx expo start
```

Then scan the QR code with the Expo Go app on your device.

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

## Key Technical Decisions

1. **React Native with TypeScript**: TypeScript is used to provide type safety throughout the application. This helps catch bugs at compile time rather than runtime, especially when working with API responses and navigation parameters. The type system makes the codebase more maintainable and reduces the likelihood of errors when refactoring or adding new features.

2. **Redux Toolkit with Redux Persist**: 
   - Redux Toolkit simplifies state management by reducing boilerplate code and providing built-in best practices
   - Redux Persist with AsyncStorage ensures the wishlist data persists across app restarts, providing a better user experience where users don't lose their saved items
   - This persistence is essential for maintaining user preferences and improving app reliability

3. **React Navigation (Static Navigation)**:
   - The static navigation configuration from React Navigation v7 provides type-safe navigation, catching navigation errors at compile time
   - Combining Stack Navigator for screen navigation and Tab Navigator for main tabs creates a native app feel with smooth transitions
   - Type-safe navigation prevents runtime errors from incorrect route names or missing parameters

4. **Axios for API Calls**:
   - A centralized API service layer using Axios keeps all API logic organized in one place, making it easier to maintain and update
   - The class-based structure (`ProductsApi`) provides a clean interface for adding new endpoints and makes the code more scalable
   - Configuring the base URL centrally makes it simple to swap out the backend API or switch between development and production environments

5. **Component Architecture**:
   - Reusable components (ProductListComponent, CategoryComponent, ReviewComponent) follow the DRY principle, reducing code duplication
   - Each screen manages its own state and API calls, keeping concerns separated and making the code easier to understand and maintain
   - This component separation enables easy reuse across different screens and simplifies testing

6. **Safe Area Context**: The `react-native-safe-area-context` library properly handles device-specific safe areas (notches, status bars) across different devices. This ensures the app's UI is correctly positioned on all devices, especially newer iPhones with notches, preventing content from being obscured by system UI elements.

7. **React Native Vector Icons**: Ionicons are used for tab bar icons because they're well-maintained, scalable, and provide a consistent visual design across the app. Vector icons scale perfectly at any size and maintain crisp quality on all screen densities.

## Improvements with More Time

With additional development time, the following improvements would enhance the app's functionality, performance, and user experience:

1. **Better Error Handling & User Feedback**:
   - Currently, errors are primarily logged to the console. Error boundaries would catch React errors gracefully and display user-friendly error screens
   - Toast notifications (using libraries like `react-native-toast-message`) would provide immediate feedback for user actions like adding items to wishlist or handling search failures
   - For API failures, retry buttons and more descriptive error messages would improve the user experience instead of generic "Failed to load" messages

2. **Performance Optimizations**:
   - Product images reload on every screen visit, which impacts performance. Image caching using `react-native-fast-image` or similar libraries would significantly improve load times and reduce bandwidth usage
   - Loading all products at once can be slow. Implementing pagination or infinite scroll would improve initial load time and reduce memory usage
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
