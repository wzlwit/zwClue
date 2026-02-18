# Custom Widget Template

Template for creating a new PyQt6 custom widget.

## Instructions

When asked to create a custom widget:

1. Create a new file under `src/widgets/{widget_name}.py`
2. Subclass the appropriate Qt base class (e.g. `QWidget`, `QPushButton`, `QFrame`)
3. Add an `__init__` method that sets up the layout and child widgets
4. Define custom signals if the widget needs to communicate state changes
5. Import and add the widget to the parent layout or main window

## Template

```python
from PyQt6.QtWidgets import QWidget, QVBoxLayout
from PyQt6.QtCore import pyqtSignal


class {WidgetName}(QWidget):
    # Define custom signals
    # value_changed = pyqtSignal(str)

    def __init__(self, parent=None):
        super().__init__(parent)
        self._setup_ui()

    def _setup_ui(self):
        layout = QVBoxLayout(self)
        # Add child widgets here
```
