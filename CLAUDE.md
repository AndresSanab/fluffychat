# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FluffyChat is a Matrix chat client written in Flutter. It's a cross-platform messaging app that supports end-to-end encryption, group chats, file sharing, and the full Matrix protocol feature set.

## Architecture

- **Flutter App**: Multi-platform client using Material Design 3
- **Matrix SDK**: Uses the `matrix` package for Matrix protocol implementation
- **Encryption**: Vodozemac library for Matrix E2E encryption (WebAssembly/Rust-based)
- **State Management**: Provider pattern for state management
- **Localization**: Built-in Flutter i18n with Weblate translations
- **Storage**: SQLite with SQLCipher for encrypted local storage

### Directory Structure

- `lib/pages/` - UI pages and views (follows page/controller pattern)
- `lib/widgets/` - Reusable UI components
- `lib/utils/` - Utility functions and extensions
- `lib/config/` - App configuration and constants
- `lib/l10n/` - Generated localization files (auto-generated, don't edit)
- `scripts/` - Build and deployment scripts
- `assets/` - Static assets including sounds and Vodozemac WASM binaries

## Common Development Commands

### Basic Flutter Commands
```bash
flutter run                          # Run in debug mode
flutter run -d chrome --web-port 8080  # Run web version
flutter build apk --release          # Build Android APK
flutter test                         # Run unit tests
flutter test integration_test/       # Run integration tests
```

### Linting and Analysis
```bash
flutter analyze                      # Run static analysis
dart format lib/ test/              # Format Dart code
flutter pub run import_sorter:main  # Sort imports
```

### Dependencies and Build Prep
```bash
flutter pub get                     # Get dependencies
flutter pub upgrade                 # Upgrade dependencies
./scripts/prepare-web.sh            # Prepare Vodozemac WASM for web
```

### Platform-Specific Builds
```bash
# Web (requires prepare-web.sh first)
flutter build web --release

# Android
./scripts/prepare-android-release.sh

# Windows
./scripts/build-windows.ps1

# iOS 
./scripts/build-ios.sh

# macOS
./scripts/build-macos.sh
```

### Integration Testing
Integration tests require Matrix homeserver setup:
```bash
./scripts/integration-prepare-host.sh      # Setup host environment
./scripts/integration-server-synapse.sh    # Start Synapse server
./scripts/integration-server-dendrite.sh   # Or start Dendrite server
flutter test integration_test/
```

## Code Style and Conventions

- Follows Flutter/Dart conventions with custom linting rules defined in `analysis_options.yaml`
- Requires trailing commas for better formatting
- Uses provider pattern for state management
- Page structure: each page has a controller and view file
- Import sorting is enforced via `import_sorter`
- Matrix client integration through `ClientManager` utility

## Key Technical Details

### Matrix Integration
- `ClientManager` handles Matrix client lifecycle and multiple accounts
- Background sync and push notifications supported on Android
- E2E encryption via Vodozemac (Rust/WASM)
- Cross-signing and device verification implemented

### Platform Support
- Mobile: Android/iOS with native features (notifications, sharing, etc.)
- Desktop: Windows, macOS, Linux
- Web: Full PWA support with WASM crypto

### Web Deployment Notes
- Requires running `./scripts/prepare-web.sh` before building for web
- This script builds Vodozemac Rust crypto library to WASM
- Web build assets go to `assets/vodozemac/` directory

## Development Workflow

1. Standard Flutter development workflow applies
2. For web builds, always run prepare-web.sh first
3. Integration tests require homeserver setup (see scripts)
4. Translations managed through Weblate (don't edit l10n files directly)
5. Uses SQLCipher for encrypted local storage across platforms