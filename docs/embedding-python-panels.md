# Embedding a Python Panel in an HDA Interface

Houdini 22 can replace an HDA's ordinary Parameter Editor with a custom
PySide6 Python Panel. The panel remains external to the HDA and is associated
with it by operator type.

## 1. Create the panel

Place a `.pypanel` file in a `python_panels` directory on `$HOUDINI_PATH`:

```text
MyPackage/
├── otls/my_asset.hdalc
└── python_panels/my_asset.pypanel
```

A minimal panel definition is:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<pythonPanelDocument>
  <interface name="MyAssetPanel" label="My Asset">
    <script><![CDATA[
import hou
from hutil.Qt import QtWidgets

widget = None

def onCreateInterface():
    global widget
    widget = QtWidgets.QLabel("Hello from my HDA")
    return widget

def onNodePathChanged(node):
    # `node` is the HDA currently shown in the Parameter Editor.
    pass
    ]]></script>

    <showInParametersPane optype="Scy::Cop/my_asset::1.0"/>
  </interface>
</pythonPanelDocument>
```

The important line is `showInParametersPane`. Its operator pattern uses:

```text
namespace::Category/operator_name::version
```

For Color Wheels this is:

```xml
<showInParametersPane optype="Scy::Cop/color_wheels::1.0"/>
```

## 2. Drive normal HDA parameters

Keep the actual state as ordinary HDA parameters and let Qt act only as their
custom view/controller:

```python
def onNodePathChanged(node):
    global current_node
    current_node = node

def set_amount(value):
    with hou.undos.group("Set Amount"):
        current_node.parm("amount").set(value)
```

This preserves parameter saving, animation, expressions, presets, undo, and a
functional conventional interface when the custom panel is unavailable.

## 3. Reload while developing

Restart Houdini, use the Python Panel Editor, or reload directly:

```python
hou.pypanel.installFile("D:/path/to/python_panels/my_asset.pypanel")
```

Navigate to another node and back to reconstruct the updated widget.

For portable distribution, include both the HDA and `python_panels` directory
in the same Houdini package. Shipping the HDA alone does not include the custom
interface.
