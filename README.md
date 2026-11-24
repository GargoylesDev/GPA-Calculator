# GPA Calculator

A Flutter app for the IT53002FP Mobile Apps Development project. Enter your modules with their
credit units and grades, and the app works out your cumulative GPA, shows which modules are
strong or weak, and helps you plan for a target GPA.

## How the GPA is calculated

```
GPA = sum(credit units × grade scale) ÷ sum(credit units)
```

Grade scale (Table 1 of the brief): A = 4, B = 3, C = 2, D = 1, E = 1, F = 0.
The brief's Figure 2 sample (4 CU B, 3 CU A, 2 CU C, 3 CU B) gives 37 ÷ 12 = **3.083**.

## Features

**Calculator**
- Add modules with a title, credit units (1–20), grade and semester.
- Duplicate titles are blocked (ignoring case), and errors show under each field.
- Tap a module to edit it. Deleting shows an Undo button.
- Calculate GPA shows the cumulative GPA to 3 decimal places, counting up to the value.
- Share a text summary of your GPA and modules.

**Statistics**
- Share of credits at Strong (A/B), Fair (C) and Weak (D/E/F) results.
- Best module, and the **Biggest impact**: the module whose one-grade rise would lift your GPA
  the most. This weighs credits as well as grade, so a 4 CU C can matter more than a 1 CU D.
- GPA for each semester, with a bar for each, plus the overall GPA.
- **Target GPA planner**: enter a target and the credits you have left to see the average you
  need: `(target × (current credits + remaining) − current points) ÷ remaining`.
  Above 4 means out of reach; 0 or below means it's already secured.
- **What-if mode**: tap a module's grade to try another and see the projected GPA.
  Your real modules are not changed.

**Profiles**
- The avatar at the top of every page opens a dropdown of profiles. Pick one to switch to it,
  or choose New profile to add one. Each profile has its own name and modules.

**Account**
- The open profile's name and initials, totals, and the grade scale.
- Edit name, and Clear all modules (asks first).

Every profile, and which one was open, is saved on the device, so they're still there after
closing the app. Data saved by the version before profiles is loaded as one profile.

One quirk of Table 1: D and E are both worth 1, so raising an E to a D doesn't change the GPA.
Biggest impact skips that step.

## Project structure

```
lib/
├── main.dart          app start-up
├── theme/             colours, fonts and theme
├── models/            Module, Profile, grade scale and GpaStore (data and GPA maths)
├── data/              profile_storage.dart: saving and loading profiles on the device
├── utils/             date text
├── widgets/           shared pieces: cards, nav bar, module form, profile menu, target planner
└── pages/             splash, calculator, statistics, account
integration_test/      automated UI test (Lab 06 format)
test/                  unit and widget tests
```

## Running

```bash
flutter pub get
flutter run
```

## Testing

```bash
flutter test                                              # unit and widget tests
flutter test integration_test/app_test.dart -d <device>   # automated UI test on an emulator
```

The integration test prints each step as `Step No: <n>, <action>` with a `Success:` line, and
pauses 5 seconds per step. Saved data is replaced with an empty in-memory store during tests,
so they don't touch the data on your device.

## Packages and assets

- [shared_preferences](https://pub.dev/packages/shared_preferences): saving profiles and modules
- [share_plus](https://pub.dev/packages/share_plus): the share button
- [iconsax_flutter](https://pub.dev/packages/iconsax_flutter): icons
- Fonts: [Inter](https://github.com/rsms/inter) and
  [Bricolage Grotesque](https://github.com/ateliertriay/bricolage), both SIL Open Font License 1.1
  (licences in `assets/fonts/`)
