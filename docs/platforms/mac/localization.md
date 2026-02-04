# Chinese Localization Implementation for macOS Menu

## Overview
This document explains the implementation of Chinese (Simplified) localization for the OpenClaw macOS menu bar application.

## Implementation Details

### Files Added
1. **English Localization**: `apps/macos/Sources/OpenClaw/Resources/en.lproj/Localizable.strings`
   - Contains all English menu strings as the base language
   
2. **Chinese (Simplified) Localization**: `apps/macos/Sources/OpenClaw/Resources/zh-Hans.lproj/Localizable.strings`
   - Contains Chinese translations for all menu items

### Files Modified
1. **Package.swift**: Updated to include localization resource processing
   ```swift
   resources: [
       .copy("Resources/OpenClaw.icns"),
       .copy("Resources/DeviceModels"),
       .process("Resources/en.lproj"),      // Added
       .process("Resources/zh-Hans.lproj"),  // Added
   ]
   ```

2. **MenuContentView.swift**: All hardcoded strings replaced with `String(localized:)` calls
   - Connection labels (configured, remote, local)
   - Menu items (heartbeats, browser control, camera, canvas, etc.)
   - Debug menu items
   - Health and heartbeat status messages
   - Microphone settings
   - Pairing messages

## Localization Keys

### Connection Status
- `connection.unconfigured` - OpenClaw not configured state
- `connection.remote` - Remote connection state
- `connection.local` - Local connection state

### Main Menu Items
- `menu.sendHeartbeats` - Send Heartbeats toggle
- `menu.browserControl` - Browser Control toggle
- `menu.allowCamera` - Allow Camera toggle
- `menu.execApprovals` - Exec Approvals picker
- `menu.allowCanvas` - Allow Canvas toggle
- `menu.voiceWake` - Voice Wake toggle
- `menu.openDashboard` - Open Dashboard button
- `menu.openChat` - Open Chat button
- `menu.openCanvas` / `menu.closeCanvas` - Canvas panel controls
- `menu.talkMode` / `menu.stopTalkMode` - Talk Mode toggle
- `menu.settings` - Settings menu item
- `menu.debug` - Debug submenu
- `menu.about` - About OpenClaw
- `menu.updateReady` - Update ready prompt
- `menu.quit` - Quit application

### Debug Menu
- `debug.openConfigFolder` - Open config folder
- `debug.runHealthCheck` - Run health check
- `debug.sendTestHeartbeat` - Send test heartbeat
- `debug.resetRemoteTunnel` - Reset remote tunnel
- `debug.verboseLoggingOn/Off` - Verbose logging toggles
- `debug.appLogging` - App logging submenu
- `debug.fileLoggingOn/Off` - File logging toggles
- `debug.openSessionStore` - Open session store
- `debug.openAgentEvents` - Open agent events
- `debug.openLog` - Open log viewer
- `debug.sendDebugVoice` - Send debug voice text
- `debug.sendTestNotification` - Send test notification
- `debug.restartGateway` - Restart gateway
- `debug.restartOnboarding` - Restart onboarding
- `debug.restartApp` - Restart application

### Status Messages
- `health.ok` - Health status OK
- `health.loginRequired` - Login required
- `health.pending` - Health check pending
- `health.running` - Health check running
- `health.checked` - Last checked timestamp
- `heartbeat.controlDisconnected` - Control channel disconnected
- `heartbeat.sent` - Last heartbeat sent
- `heartbeat.ok` - Heartbeat OK
- `heartbeat.skipped` - Heartbeat skipped
- `heartbeat.failed` - Heartbeat failed
- `heartbeat.generic` - Generic heartbeat status
- `heartbeat.none` - No heartbeat yet

### Activity Labels
- `activity.main` - Main session
- `activity.other` - Other session

### Microphone Settings
- `mic.autoDetect` - Auto-detect microphone
- `mic.systemDefault` - System default
- `mic.disconnected` - Microphone disconnected
- `mic.refreshing` - Refreshing microphone list
- `mic.label` - Microphone menu label

### Pairing
- `pairing.pending` - Pairing approval pending
- `pairing.repair` - Repair action
- `pairing.devicePending` - Device pairing pending

### Alerts
- `alert.dashboardUnavailable` - Dashboard unavailable message
- `alert.remoteTunnel` - Remote tunnel alert title

## How It Works

The app uses SwiftUI's built-in localization system:
- `String(localized: "key")` looks up the string in the appropriate `.strings` file
- macOS automatically selects the correct language based on system preferences
- Falls back to English if a translation is missing

## Testing Localization

To test the Chinese localization:

1. Build the app with Swift Package Manager
2. Change your macOS system language to Chinese (Simplified)
3. Launch the OpenClaw app
4. Right-click the menu bar icon to see the localized menu

Alternatively, you can test in Xcode by:
1. Opening the scheme editor
2. Setting "Application Language" to "Chinese, Simplified"
3. Running the app

## Adding More Languages

To add additional languages:

1. Create a new `.lproj` directory (e.g., `zh-Hant.lproj` for Traditional Chinese)
2. Copy the `Localizable.strings` file from `en.lproj`
3. Translate the values (keeping the keys unchanged)
4. Add the new directory to `Package.swift` resources
5. Rebuild the app

## Translation Notes

The Chinese translations follow these principles:
- Concise and clear terminology
- Consistent with macOS UI conventions
- Technical terms are kept readable while maintaining accuracy
- Action-oriented phrases (e.g., "打开" for "Open", "发送" for "Send")
