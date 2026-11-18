# Changelog

All notable changes are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/),
versions follow [Semantic Versioning](https://semver.org/).

## [0.1.1] - 2026-11-18

First public release (0.1.0 was an internal build and was never published).

### Added
- Seven native mini-games, written twice (Swift for iOS, Kotlin for Android): `penalty-flick`,
  `crossbar-challenge`, `keepy-uppy`, `hockey-shootout`, `top-shelf`, `table-hockey`, `buzzer-beater`.
- Expo module `@spectado/embed-games` (Expo SDK 53 or newer): `openGame()`, `<SpectadoGameView />`,
  `getAvailableGames()`, `getBestScore()` / `resetBestScore()`, `isAvailable()`.
- Swift module `SpectadoEmbedGames` (SwiftUI, UIKit) and Android library `com.spectado:embed-games`
  (Activity, View, `ActivityResultContract`).
- Theming (colours, team name, logo), cs / sk / en localisation (region tags such as `cs-CZ` are accepted),
  per-game best score persistence.
- One result object on every platform. The full-screen APIs report exactly once, also when the host app
  takes the game screen away itself (`completed: false` with the play so far).
- `isPausedByHost` on both `SpectadoGameView`s: a pause the player cannot lift. The Expo `paused` prop uses it.
- A small "spectado.com" link on the ready, pause and result screens of every game (hidden during play);
  it opens https://spectado.com in the browser.
- Binary distribution from the public `spectado-embed-games-dist` repository: `SpectadoEmbedGames.xcframework`
  through Swift Package Manager, a minified AAR in a static Maven repository, and a binary Expo package.
- README with step-by-step integration for Expo, Swift and Kotlin, a reference for every game (controls,
  scoring, length, options, result `details`), customisation and lifecycle notes, and screenshots.
