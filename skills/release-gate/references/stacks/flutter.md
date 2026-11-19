# Flutter release items

- Version: `version: x.y.z+build` in `pubspec.yaml`. The build number must increase for every store upload.
- Android: signing config and keystore location (never committed), `minSdk` and `targetSdk` meet Play requirements, permissions reviewed, `flutter build appbundle --release`.
- iOS: signing and provisioning, bundle id, privacy manifest and usage strings, `flutter build ipa --release`.
- Crash and debug symbols uploaded if obfuscation is on (`--obfuscate --split-debug-info`).
- Store listing: release notes, screenshots, data-safety and privacy answers match the app.
- Staged rollout percentage chosen. Remote kill switch or minimum-version gate exists for a bad build.
- `flutter pub outdated` and a dependency audit reviewed.
