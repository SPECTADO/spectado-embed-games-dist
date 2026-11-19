# Changelog

All notable changes are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/),
versions follow [Semantic Versioning](https://semver.org/).

## [0.2.1] - 2026-11-19

Documentation only: the binaries are rebuilt from the same code as 0.2.0.

### Documentation

- README: how to follow the newest release on each channel (Expo update command, SPM `from:`, Gradle
  `latest.release`) and how to pin one version.

## [0.2.0] - 2026-11-19

A gameplay change: the shooting games are now controlled by a true swipe and are harder. There is **no API
change**: game ids, `GameConfig`, `GameResult` and the `details` keys are the same as in 0.1.1, so no host code
has to change. Players will notice the new controls, and scores will be lower than in 0.1.1.

### Changed
- Shots are now taken with a true swipe (flick) in `penalty-flick`, `crossbar-challenge`, `hockey-shootout`,
  `top-shelf` and `buzzer-beater`. Only the quick final motion of the finger counts: its direction aims and
  its speed (not the length of the stroke) sets the power. There is no target ring, trajectory preview, aim
  line or power read-out while the finger is down. A slow drag-and-release, a finger that stops before it
  lifts, or a swipe away from the goal does not shoot; after two such tries a small "Swipe faster!" reminder
  appears (en / cs / sk), or "Swipe up!" when the swipe went the wrong way. The swipe may start anywhere in
  the lower part of the play area, so the games are comfortable to play with one hand.
- A swipe is a release of at least 900 points per second that covers at least 50 points; a deliberate
  drag-and-release (for example 220 points in a quarter of a second) and a short twitch at the end of a
  slow drag do not shoot. The finger is measured in points (iOS pt, Android dp), so the same flick is the
  same shot on a small phone, a large phone and a tablet. Above 2,600 points per second extra speed counts
  for less and less: a hard flick lands high, only a very hard one (about 3,500 and more) goes over.
- A finger that touches the screen a moment before the next ball or puck is ready, and flicks once it is,
  shoots. A swipe released while the ball is away still does nothing. A finger resting on the screen
  (a gripping thumb) no longer blocks the swipes of another finger. A finger held down through a pause can
  flick after the resume.
- The "spectado.com" link on the ready screen reacts to a tap only: a swipe that starts on it shoots.
- `penalty-flick`: the speed of the flick sets pace and height (too hard goes over the bar), a curved flick
  bends the ball, and the goalkeeper is re-tuned for the new control: a soft roll along the ground is an
  easy save. The result says "Well played" from 2 goals (was 3).
- `crossbar-challenge`: the speed of the flick sets the height (a hard flick reaches the crossbar, harder goes
  over), a curved flick bends the ball, the hidden assist near the crossbar, posts and top bins is smaller,
  and the result thresholds are lower (good 900, great 2,800 points).
- `hockey-shootout`: the slingshot is gone. Swipe the puck towards the net: the speed sets the power (a harder
  shot flies higher and gives the goalie less time, too hard goes over the net), and a curved swipe is the
  deke (the puck swerves and the goalie goes the wrong way). A shot can now hit the crossbar or go over, and
  the goalie is re-tuned. Keeping goal against the CPU (drag left / right) is unchanged.
- `top-shelf`: the direction of the flick aims left or right and only its speed sets how high the puck lands;
  the landing preview is gone and the hidden assist near the targets is smaller.
- `buzzer-beater`: only the speed of the flick sets how far the ball goes; the aiming arc is gone and the
  hidden aim assist is smaller.
- The tutorial hints of these five games describe the swipe (en / cs / sk).
- README: the controls of the five games, and the screenshots.
- Not changed: `keepy-uppy` (tap the ball) and `table-hockey` (drag the paddle) keep their controls.

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
