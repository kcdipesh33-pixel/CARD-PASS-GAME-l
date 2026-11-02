# CARD PASS – Play, Pass, Win
## Complete Flutter Android Offline Multiplayer Game

### 1. Offline Hotspot Networking Architecture
This game requires **zero internet**, **no Firebase**, and **no cloud servers**.
It communicates completely over local Wi-Fi / Hotspot using WebSockets.

1. **Host Phone**:
   - Turns ON Android **Mobile Hotspot** in Android Settings.
   - Default Android Hotspot Gateway IP is `192.168.43.1`.
   - The Host launches Card Pass, enters the Owner PIN, and starts the game.
   - The app displays a **QR Code** and the local IP address (`192.168.43.1:8080`).

2. **Player Phones**:
   - Connect to the Host's Wi-Fi hotspot in Android Wi-Fi settings (no mobile data required!).
   - Open Card Pass -> Tap **JOIN GAME**.
   - Either scan the Host's QR Code or type `192.168.43.1:8080`.
   - Tap **Connect & Play**.

---

### 2. How to Build & Install the Android APK

#### Prerequisites:
- Install Flutter SDK (version 3.0+) from https://flutter.dev
- Install Android Studio or Android Command Line Tools with Android SDK Platform 33/34.

#### Build Commands:
```bash
# 1. Navigate to the flutter_card_pass folder
cd flutter_card_pass

# 2. Get dependencies
flutter pub get

# 3. Build optimized Release APK
flutter build apk --release

# The installable APK will be generated at:
# build/app/outputs/flutter-apk/app-release.apk
```

#### Installing on Android Phones:
1. Transfer `app-release.apk` to phones via USB cable, Nearby Share, or Bluetooth.
2. On each Android phone, open the APK file in Files / Downloads.
3. If prompted, enable **"Install unknown apps"** for Files or Chrome.
4. Tap **Install** and launch **CARD PASS**!

---

### 3. Host Security & Offline APK Limitations
- **Owner Authentication**: The Host Control Panel requires the owner PIN (`7777` by default, customizable in settings/build).
- **Control Only**: Host does not receive cards and cannot participate as a player.
- **Offline Security Explanation**:
  In a 100% offline APK without a cloud server, the password hash and host logic reside locally inside the compiled Dart AOT binary. While standard players cannot access the Host without the correct password, a sophisticated reverse engineer decompiling APK bytecode could theoretically patch the check. Obfuscation (`flutter build apk --obfuscate --split-debug-info=...`) is applied to protect against decompilation.
