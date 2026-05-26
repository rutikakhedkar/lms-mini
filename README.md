# EduTech LMS - React Native Expo App

A Mini LMS (Learning Management System) built with React Native Expo.

## Tech Stack

- **Framework**: React Native Expo (SDK 56)
- **Language**: TypeScript (strict mode)
- **Navigation**: Expo Router (file-based routing)
- **Auth Storage**: Expo SecureStore (tokens), AsyncStorage (app data)
- **Forms**: React Hook Form + Zod validation
- **Images**: Expo Image (with caching)
- **Notifications**: Expo Notifications
- **Offline**: @react-native-community/netinfo
- **API**: [freeapi.app](https://api.freeapi.app)

## Features

- **Auth** — Register/Login with JWT, auto-login on restart, secure token storage
- **Course Catalog** — Browse courses from freeapi.app with search & pull-to-refresh
- **Bookmarks** — Save courses locally; notification when 5+ bookmarked
- **Enroll** — Enroll in courses with visual feedback
- **WebView** — Course content viewer with Native ↔ WebView messaging
- **Profile** — View user info and stats
- **Offline Banner** — Detects and displays no-connection state
- **Notifications** — Reminder if app not opened for 24 hours
- **Error Handling** — Retry logic, timeout, user-friendly errors

## Folder Structure

```
app/
  (auth)/      # login & register screens
  (tabs)/      # main tabs: courses, bookmarks, profile
  course/[id]  # course detail screen
  webview      # WebView content screen
components/    # CourseCard, SearchBar, OfflineBanner
constants/     # API endpoints, color palette
hooks/         # useNetworkStatus
providers/     # AuthProvider, CourseProvider
store/         # authStore, courseStore (context + helpers)
utils/         # api client (fetch + retry), notifications
```

## Setup & Run

```bash
# Install dependencies
npm install

# Start Expo
npx expo start

# Run on Android
npx expo start --android

# Run on iOS
npx expo start --ios
```

## API Endpoints Used

| Purpose | Endpoint |
|---|---|
| Register | `POST /api/v1/users/register` |
| Login | `POST /api/v1/users/login` |
| Logout | `POST /api/v1/users/logout` |
| Current User | `GET /api/v1/users/current-user` |
| Courses | `GET /api/v1/public/randomproducts` |
| Instructors | `GET /api/v1/public/randomusers` |

## Key Architectural Decisions

- **Expo Router** for file-based navigation — simpler than React Navigation config
- **Context + useReducer** for auth state — avoids external state library overhead
- **SecureStore** for tokens, **AsyncStorage** for bookmarks/enrollments
- **Fetch with retry** — built-in retry (2 attempts) + 10s timeout on every request
- **Memoized components** — `CourseCard` wrapped in `memo`, filtered list in `useMemo`
