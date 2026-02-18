# Custom Dialog Template

Template for creating a new PyQt6 dialog window.

## Instructions

When asked to create a dialog:

1. Create a new file under `src/dialogs/{dialog_name}.py`
2. Subclass `QDialog`
3. Include accept/reject buttons where appropriate
4. Return results via `self.accept()` and accessor methods

## Template

```python
from PyQt6.QtWidgets import (
    QDialog, QVBoxLayout, QHBoxLayout,
    QPushButton, QLabel
)


class {DialogName}(QDialog):
    def __init__(self, parent=None):
        super().__init__(parent)
        self.setWindowTitle("{DialogName}")
        self._setup_ui()

    def _setup_ui(self):
        layout = QVBoxLayout(self)

        # Add content here
        layout.addWidget(QLabel("Content goes here"))

        # Button row
        btn_layout = QHBoxLayout()
        ok_btn = QPushButton("OK")
        cancel_btn = QPushButton("Cancel")
        ok_btn.clicked.connect(self.accept)
        cancel_btn.clicked.connect(self.reject)
        btn_layout.addWidget(ok_btn)
        btn_layout.addWidget(cancel_btn)
        layout.addLayout(btn_layout)

    def get_result(self):
        """Return dialog result after accept."""
        return None
```
