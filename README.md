# EasyWallet - Multiplatform Decentralized Wallet

[![Github Release](https://github.com/BreakZero/EasyWallet-Multiplatform/actions/workflows/Release.yml/badge.svg)](https://github.com/BreakZero/EasyWallet-Multiplatform/actions/workflows/Release.yml)
[![Check Code Style](https://github.com/BreakZero/EasyWallet-Multiplatform/actions/workflows/CheckCodeStyle.yml/badge.svg)](https://github.com/BreakZero/EasyWallet-Multiplatform/actions/workflows/CheckCodeStyle.yml)

## Project Overview

EasyWallet is a decentralized wallet application built with Kotlin Multiplatform, supporting both Android and iOS platforms. The project follows Clean Architecture design principles, with all wallet-related data stored locally. It uses user-defined RPC nodes to ensure higher trustworthiness and privacy.

### Core Features

- 🔐 **Mnemonic Management**: Support for wallet creation via mnemonic import or generation
- 🌐 **Multi-chain Support**: Currently supports Ethereum chain, with architecture designed for multi-chain expansion
- 📱 **Cross-platform**: Built on Kotlin Multiplatform, supporting Android and iOS
- 🔒 **Local Storage**: All sensitive data is stored locally to protect user privacy
- 🎨 **Modern UI**: Using Jetpack Compose (Android) and SwiftUI (iOS)
- 📊 **Market Data**: Integrated CoinGecko API for cryptocurrency market information
- 📰 **News Browsing**: BlockChair API integration for blockchain news

## Project Architecture

### Overall Architecture

The project adopts Clean Architecture + MVI/MVVM architectural pattern, divided into the following main modules:

```
EasyWallet-Multiplatform/
├── composeApp/              # Android application main module
├── iosApp/                  # iOS application main module
├── platform/                # Shared business logic layer
│   ├── model/              # Data model layer
│   ├── domain/             # Business logic layer
│   ├── data/               # Data access layer
│   ├── network/            # Network request layer
│   ├── database/           # Local database layer
│   └── datastore/          # Data storage layer
├── build-logic/            # Build logic configuration
└── configs/                # Configuration files
```

### Architecture Diagram

![architecture.png](screenshots%2Farchitecture.png)

### Detailed Module Description

#### 1. Platform Layer (Shared Business Logic)

**model module**
- Defines all data models and entity classes
- Contains data models for network requests, database, UI presentation, and other layers
- Uses Kotlinx Serialization for serialization

**domain module**
- Contains business logic and Use Cases
- Defines Repository interfaces
- Handles business rules and data transformations

**data module**
- Implements Repository interfaces
- Coordinates network layer, database layer, and data storage layer
- Handles data source switching and caching strategies

**network module**
- Uses Ktor for network requests
- Supports Android (OkHttp) and iOS (Darwin) platforms
- Integrates API key management (BuildKonfig)

**database module**
- Uses SQLDelight for local database management
- Supports multi-chain data storage
- Provides coroutine extension support

**datastore module**
- Uses DataStore for lightweight data storage
- Stores user preferences and application configuration

## Tech Stack & Third-party Libraries

### Core Frameworks

| Technology           | Version | Purpose                     |
|---------------------|---------|------------------------------|
| Kotlin Multiplatform | 2.2.10  | Cross-platform development framework |
| Jetpack Compose      | 1.8.2   | Android UI framework         |
| SwiftUI              | -       | iOS UI framework             |
| Kotlin Coroutines    | 1.10.2  | Asynchronous programming     |

### Network & Data

| Library               | Version       | Purpose              |
|-----------------------|---------------|----------------------|
| Ktor                  | 3.3.0         | HTTP client          |
| Kotlinx Serialization | 1.9.0         | JSON serialization   |
| SQLDelight            | 2.1.0         | Local database       |
| DataStore             | 1.1.7         | Lightweight data storage |
| Paging3               | 3.3.0-alpha02 | Pagination loading   |

### Dependency Injection & Architecture

| Library             | Version    | Purpose                  |
|---------------------|------------|--------------------------|
| Koin                | 4.1.1      | Dependency injection framework |
| Navigation Compose  | 2.9.0-rc02 | Page navigation          |
| Lifecycle ViewModel | 2.9.3      | Lifecycle management     |

### UI & Images

| Library | Version | Purpose              |
|---------|---------|----------------------|
| Coil    | 3.3.0   | Image loading        |
| Vico    | 2.1.3   | Chart rendering      |
| QR Kit  | 3.1.3   | QR code generation/scanning |
| Haze    | 1.6.10  | Visual effects       |

### Blockchain & Cryptography

| Library     | Version | Purpose                    |
|-------------|---------|----------------------------|
| Wallet Core | 4.3.9   | Blockchain wallet core functionality |
| BigNum      | 0.3.10  | Big number operations      |

### Development Tools

| Tool        | Version | Purpose               |
|-------------|---------|----------------------|
| Ktlint      | 13.1.0  | Code formatting       |
| BuildKonfig | 0.17.1  | Build configuration generation |
| Kermit      | 2.0.8   | Logging               |

## Project Structure Details

### Directory Structure

```
EasyWallet-Multiplatform/
├── .github/                 # GitHub Actions configuration
├── .githooks/              # Git hook scripts
├── .gradle/                # Gradle cache
├── .idea/                  # IDE configuration
├── build-logic/            # Custom build logic
│   ├── convention/         # Gradle convention plugins
│   └── building.versions.toml  # Version management
├── composeApp/             # Android application
│   ├── src/
│   │   ├── androidMain/    # Android-specific code
│   │   ├── commonMain/     # Shared code
│   │   └── iosMain/        # iOS-specific code
│   └── build.gradle.kts
├── iosApp/                 # iOS application
│   ├── iosApp/            # iOS project files
│   ├── Podfile            # CocoaPods dependencies
│   └── iosApp.xcodeproj/  # Xcode project
├── platform/              # Shared business logic
│   ├── model/             # Data models
│   ├── domain/            # Business logic
│   ├── data/              # Data access
│   ├── network/           # Network requests
│   ├── database/          # Database
│   └── datastore/         # Data storage
├── configs/               # Configuration files
│   ├── package_read.properties  # GitHub package authentication
│   └── apikeys.properties      # API key configuration
├── screenshots/           # Application screenshots
├── scripts/               # Build scripts
├── keystore/              # Signing keys
├── build.gradle.kts       # Root build script
├── settings.gradle.kts    # Project settings
├── gradle.properties      # Gradle properties
└── libs.versions.toml     # Dependency version management
```

### Key Configuration Files

#### 1. Dependency Version Management (libs.versions.toml)
Centrally manages all third-party library versions to ensure dependency consistency.

#### 2. Build Logic (build-logic/)
Custom Gradle plugins to simplify build configuration for each module.

#### 3. API Key Configuration
- `configs/package_read.properties`: GitHub package authentication
- `configs/apikeys.properties`: Third-party API keys

## Development Environment Setup

### Prerequisites

- Android Studio Hedgehog 2023.1.1+
- Xcode 15.0+
- Kotlin 2.2.10+
- Gradle 8.12.2+

### Setup Steps

1. **Clone the project**
```bash
git clone https://github.com/BreakZero/EasyWallet-KMP.git
cd EasyWallet-Multiplatform
```

2. **Configure GitHub authentication**
Create a `package_read.properties` file in the `configs/` directory:
```properties
gpr.name=Your Github Name
gpr.key=Your Github token
```

3. **Configure API keys**
Create an `apikeys.properties` file in the `configs/` directory:
```properties
etherscan=YOUR_ETHERSCAN_API_KEY
coingecko=YOUR_COINGECKO_API_KEY
opensea=YOUR_OPENSEA_API_KEY
```

4. **Generate build configuration**
```bash
./gradlew -p platform generateBuildKonfig
```

5. **Build the project**
```bash
# Android
./gradlew :composeApp:assembleDebug

# iOS
cd iosApp && pod install
# Then open iosApp.xcworkspace in Xcode
```

## Feature Modules

### Implemented Features

- ✅ Mnemonic import/generate wallet
- ✅ Ethereum chain asset management
- ✅ Local data storage
- ✅ Multi-chain database architecture
- ✅ Modern UI interface
- ✅ Dependency injection architecture

### In Development/Planned Features

- 🚧 Full iOS functionality
- 🚧 More blockchain support
- 🚧 Transaction history viewing
- 🚧 Custom token addition
- 🚧 Advanced security features

## Contributing Guide

1. Fork the project
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Create a Pull Request

## Acknowledgements

- [Trust Wallet Core](https://github.com/trustwallet/wallet-core) - Blockchain wallet core functionality
- [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html) - Cross-platform development framework
- [Jetpack Compose](https://developer.android.com/jetpack/compose) - Modern Android UI framework
- [CoinGecko](https://www.coingecko.com/) - Cryptocurrency market data
- [BlockChair](https://blockchair.com/) - Blockchain data service

---
