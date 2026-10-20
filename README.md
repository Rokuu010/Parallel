# Parallel

**A private space for two people who are close but apart.**

Parallel is a mobile app for long-distance couples. It isn't a chat app or a dating app: two people pair privately with a code, and everything inside is just for the two of them. Every feature is built around one idea: making the other person feel thought about, even when you're far away.

> 🔒 **The source code is private** because the app is heading for the App Store. This repo is a showcase of what it does and how it's built. I'm happy to walk through the code in an interview.

<p align="center">
  <img src="screenshots/feels.png" width="200" alt="Answering a daily question together">
  <img src="screenshots/us.png" width="200" alt="Shared photo of the day, watch list and bucket list">
  <img src="screenshots/same-time.png" width="200" alt="Same time: hold together to connect">
  <img src="screenshots/miss-me.png" width="200" alt="Sealed notes for when you miss me">
</p>

## Features

- **Pair privately.** One partner creates a code and the other enters it. There's no feed and there are no strangers.
- **Answer together.** Daily questions, "would you rather" and a scored couples quiz. Answers stay hidden until you've both replied, then they're revealed side by side.
- **Photo of the day.** You each post one photo a day, and you only see each other's once you've both posted.
- **Leave things to find later.** Write notes, record voice notes and share songs. The "For when you miss me" space holds sealed notes, photos and voice messages for your partner to open when they need them.
- **Plan together.** A shared watch list and bucket list.
- **Same time.** The app shows when you're both in it at once. Hold the screen together to fill a glowing halo, with haptic feedback and a heart burst when it completes.
- **Light and dark mode** throughout, with a soft, frosted-glass design.

## Engineering highlights

- **Real-time presence.** "Same time" detects when both partners are active using heartbeat timestamps in Firestore.
- **Parallel game rounds.** The question games started out sharing a single Firestore document. I refactored them so each mode has its own document, which lets several games run at once without overwriting each other.
- **Theme system.** Every colour is a theme token, so the whole app switches cleanly between light and dark mode.

## Security

Couples share private photos, notes and voice messages, so security was designed in from the start:

- **Firestore security rules** deny by default. Each couple can only read and write their own data.
- **Pairing codes** are single-use, expire after an hour, and can't be used to join an account that's already paired.
- **Uploads** to Cloudinary are restricted to specific image and audio formats. Images are capped in size, and every file gets an unguessable ID.
- **Firebase Auth** has email enumeration protection turned on and enforces a minimum password length.
- **Tested with a second account.** This found a pairing bug where the app tried to read data that the new security rules (correctly) blocked. I fixed the pairing flow without loosening the rules.

## Tech stack

| Part | Technology |
|---|---|
| Mobile app | React Native, Expo |
| Database and real-time sync | Firebase Firestore |
| Accounts | Firebase Auth |
| Photo and voice storage | Cloudinary |

## Status

Feature-complete and being prepared for release on the iOS App Store.

## Author

Built by [Rohan](https://github.com/Rokuu010).
