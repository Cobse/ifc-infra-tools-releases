# Installing IfcGH

IfcGH adds an **IfcGH** tab to Grasshopper with five components that export
Rhino geometry and reinforcement to IFC 4.3:

| Component | Does |
| --- | --- |
| IfcPropsFromExcel | Reads a property workbook (.xlsx) into a property table |
| IfcGeomComposer | Turns a Brep into a host element (slab, wall, ...) |
| IfcRebarAttributes | Rebar size/grade/mandrel, position, spacing, hooks |
| IfcRebarGroupComposer | Groups rebar curves in a host element |
| IfcExport | Writes everything to an `.ifc` file |

## Requirements

- Windows, **Rhino 8** (tested with Rhino 8 SR36; keep Rhino up to date via
  *Help > Check for Updates*). Rhino 7 and macOS are not supported.
- Internet access (or a proxy that allows `pypi.org`) the first time a
  component runs - see [First run](#first-run).

## Install

1. Download the latest `ifcgh-<version>-rh8-any.yak` from
   [Releases](https://github.com/Cobse/ifc-infra-tools-releases/releases).
2. Close Grasshopper, then either
   - drag the `.yak` file onto the Rhino viewport, or
   - run in a terminal:
     `"C:\Program Files\Rhino 8\System\Yak.exe" install <path>\ifcgh-<version>-rh8-any.yak`
3. Restart Rhino and open Grasshopper. The components are on the **IfcGH** tab.

## First run

The first time an IfcGH component solves, Rhino downloads `ifcopenshell` and
`openpyxl` from PyPI into its Python environment. This takes a minute or two
(the `ifcopenshell` download is large); later runs are fast.

## Update

Install the newer `.yak` the same way, then restart Rhino.

## Uninstall

Rhino `PackageManager` command > *Installed* > IfcGH > *Uninstall*, or
`"C:\Program Files\Rhino 8\System\Yak.exe" uninstall IfcGH`. Restart Rhino.

## Troubleshooting

- **`ModuleNotFoundError: No module named 'ifcopenshell'`** - the first-run
  download failed. Check your internet/proxy access to `pypi.org`, then
  re-solve the component (right-click > *Recompute*, or F5 in Grasshopper).
- **Behaviour of an old version after updating** - restart Rhino; Python
  modules stay loaded until Rhino closes.
- **Components missing** - check `PackageManager` > *Installed* lists IfcGH,
  and that Grasshopper was restarted after installing.
