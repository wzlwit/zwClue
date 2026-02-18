# PyQt6 UI Development

Skill for building PyQt6 desktop applications. Use this when adding UI components, custom widgets, layouts, dialogs, or other GUI assets.

## Setup

1. Install PyQt6 in the active conda environment: `pip install PyQt6`
2. Add `PyQt6` to `requirements.txt` if not already listed

## Project Structure

```
src/
  main.py              — Application entry point
  widgets/             — Custom widget classes
  dialogs/             — Dialog windows
  resources/           — Icons, images, stylesheets
```

## Conventions

- Subclass `QMainWindow` for the main window in `src/main.py`
- Place each custom widget in its own file under `src/widgets/`
- Place dialog classes under `src/dialogs/`
- Place static assets (icons, images, `.qss` stylesheets) under `src/resources/`
- Use layouts (`QVBoxLayout`, `QHBoxLayout`, `QGridLayout`) instead of absolute positioning
- Connect signals/slots using the `widget.signal.connect(slot)` pattern
- Keep UI logic separate from business logic — widgets should emit signals, not process data directly

## Subfolders

- `widgets/` — Reusable custom widget templates
- `dialogs/` — Reusable dialog templates
- `resources/` — Default stylesheets, icons, and other assets

## User Settings Persistence

- Use `QSettings` to save and restore user input across sessions
- Initialize in `main.py`: `QSettings(QSettings.Format.IniFormat, QSettings.Scope.UserScope, "{app_name}", "{app_name}")`
- Save values with `settings.setValue("key", value)`
- Restore values with `settings.value("key", defaultValue)`
- Common use cases: window size/position, last-used form inputs, user preferences
- Call `settings.sync()` to ensure writes are flushed

## Stylesheets

- Use `.qss` files in `src/resources/` for styling
- Load stylesheets in `main.py` with `app.setStyleSheet(open("src/resources/style.qss").read())`
