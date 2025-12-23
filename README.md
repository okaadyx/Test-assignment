# Product Catalog App

A React Native mobile application for browsing and managing products. This app allows users to explore products, search by category or keyword, view detailed product information, and maintain a wishlist of favorite items.

## App Functionality

This app provides the following features:

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

The app fetches product data from the [DummyJSON API](https://dummyjson.com) and provides a smooth, native mobile experience for browsing and managing products.

## How to Run the Project

### Prerequisites

- Node.js (>=20)
- React Native development environment set up ([Set Up Your Environment](https://reactnative.dev/docs/set-up-your-environment))
- For Android: Android Studio and Android SDK
- For iOS: Xcode and CocoaPods (macOS only)

### Installation

1. Install dependencies:
```sh
npm install
# OR
yarn install
```

2. For iOS (macOS only), install CocoaPods dependencies:
```sh
cd ios
pod install
cd ..
```

### Running the App

1. Start the Metro bundler:
```sh
npm start
# OR
yarn start
```

2. In a new terminal, run the app:

**For Android:**
```sh
npm run android
# OR
yarn android
```

**For iOS (macOS only):**
```sh
npm run ios
# OR
yarn ios
```

The app will launch in the Android Emulator, iOS Simulator, or on your connected device.

### Development Tips

- Use Fast Refresh for automatic updates when you save files
- Press <kbd>R</kbd> twice (Android) or <kbd>R</kbd> in iOS Simulator to reload
- Access Dev Menu: <kbd>Ctrl</kbd> + <kbd>M</kbd> (Windows/Linux) or <kbd>Cmd ⌘</kbd> + <kbd>M</kbd> (macOS)

## Key Technical Decisions

1. **React Native with TypeScript**: Chose TypeScript for type safety and better developer experience, reducing runtime errors and improving code maintainability.

2. **Redux Toolkit with Redux Persist**: 
   - Used Redux Toolkit for efficient state management
   - Implemented Redux Persist with AsyncStorage to persist wishlist data across app restarts
   - This ensures users don't lose their saved items when the app is closed

3. **React Navigation (Static Navigation)**:
   - Used `@react-navigation/native` with static navigation configuration for type-safe navigation
   - Implemented a combination of Stack Navigator (for screens) and Tab Navigator (for main tabs)
   - This provides a native feel and smooth transitions between screens

4. **Axios for API Calls**:
   - Created a centralized API service layer using Axios
   - Organized API calls in a class-based structure for better maintainability
   - Base URL configured to use DummyJSON API

5. **Component Architecture**:
   - Separated reusable components (ProductListComponent, CategoryComponent, ReviewComponent)
   - Screens handle their own state and API calls
   - Clear separation of concerns between UI components and business logic

6. **Safe Area Context**: Used `react-native-safe-area-context` to handle device-specific safe areas (notches, status bars) properly across different devices.

7. **React Native Vector Icons**: Used Ionicons for consistent, scalable tab bar icons.

## Improvements You'd Make with More Time

1. **Error Handling & User Feedback**:
   - Implement comprehensive error boundaries
   - Add toast notifications for user actions (add to wishlist, search errors)
   - Better error messages and retry mechanisms for failed API calls

2. **Performance Optimizations**:
   - Implement image caching and lazy loading for product images
   - Add pagination or infinite scroll for product lists
   - Optimize FlatList rendering with better key extraction and memoization

3. **Enhanced Features**:
   - Add product filtering and sorting options (price, rating, etc.)
   - Implement a shopping cart functionality
   - Add user authentication and personalized recommendations
   - Implement product comparison feature

4. **Testing**:
   - Add unit tests for Redux slices and API services
   - Add integration tests for navigation flows
   - Add component tests using React Native Testing Library

5. **UI/UX Improvements**:
   - Add skeleton loaders instead of simple "Loading..." text
   - Implement pull-to-refresh functionality
   - Add animations and transitions for better user experience
   - Improve empty states with helpful illustrations or messages

6. **Code Quality**:
   - Add ESLint and Prettier configuration for consistent code style
   - Implement proper TypeScript strict mode
   - Add code documentation and JSDoc comments
   - Set up CI/CD pipeline for automated testing and deployment

7. **Offline Support**:
   - Implement offline data caching
   - Add sync mechanism when connection is restored
   - Show cached data when offline

8. **Accessibility**:
   - Add proper accessibility labels and hints
   - Ensure proper contrast ratios
   - Support screen readers
