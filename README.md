# WORK IN PROGRESS - Many updates needed. Can serve as a good reference but is not currently importing all necessary attribute fields for setting speeds/feeds.
I am currently working on correcting this to it works directly on import.

# SpeTool Fusion 360 → FreeCAD CAM

A FreeCAD 1.1 CAM tool library converted from the supplied SpeTool Fusion 360
tool database (`SpeTool-Fusion-360-Tool-File-Database-251015.tools`).

## What's included

- **225 FreeCAD ToolBits** (`Bit/*.fctb`)
- **FreeCAD library** (`Library/SpeTool-Fusion-360-Z1.fctl`)
- This README

The library is intended for **FreeCAD 1.1+**.

## Installation

Keep the directory structure intact:

```text
SpeTool_FreeCAD_Tool_Library/
├── Bit/
├── Library/
│   └── SpeTool-Fusion-360.fctl
```

In FreeCAD CAM, open the Tool Bit Library and load:

`Library/SpeTool-Fusion-360.fctl`

Do not separate the `Library` and `Bit` directories because the `.fctl` file
references the ToolBits using relative paths.

## Tool data

The conversion preserves, where supplied by Fusion:

- Tool number
- Cutter diameter
- Shank diameter
- Overall length
- Cutting length
- Flute count
- Tool material
- Vendor
- SpeTool product ID
- Product description
- Product URL
- Fusion GUID
- Original Fusion tool type and units

Fusion tool types that do not have an exact one-to-one FreeCAD ToolBit shape are
mapped to the closest standard FreeCAD representation:

| Fusion type | FreeCAD representation |
|---|---|
| Flat/end mill | End mill |
| Ball end mill | Ball end |
| Radius mill | Bullnose |
| Chamfer mill | Chamfer |
| Tapered mill | V-bit/conical approximation |

**Tapered ball-nose tools require particular care:** FreeCAD's standard V-bit
representation does not exactly model every tapered-ball geometry. Verify the
tool geometry and resulting toolpath before cutting.

## Safety

This repository is a starting-point tool-library conversion, not a guarantee
of safe machining. The operator is responsible for verifying the tool,
workholding, CAM strategy, spindle speed, feed, depth of cut, and machine
limits before running a program.

Never rely on a converted tool definition without comparing it to the physical
cutter. Always perform a simulation/verification pass and use appropriate
machine guarding and PPE.

## Source and attribution

Original tool data was supplied by the repository maintainer/user from a
Fusion 360 `.tools` database produced for SpeTool tooling.

This repository contains converted tool metadata. SpeTool names, trademarks,
product descriptions, and product links remain the property of their respective
owners.
