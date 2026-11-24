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

## IfcExport `param` keys

Connect a panel to `param` with one `key = value` per line (all optional):

| Key | Meaning |
| --- | --- |
| `IfcSchema` | IFC schema, default `"IFC4X3_ADD2"` |
| `IfcProject` | Project name |
| `IfcSite` | Site name |
| `IfcBasePoint` | Export vector `(x, y)` in mm: the real-world XY of the Rhino origin |
| `IfcBasePointExport` | How the vector is stored: `site` (default), `mapconversion` or `world` |
| `IfcCRS` | Coordinate reference system for `mapconversion`, e.g. `"EPSG:5111"` |

Model near the Rhino origin and let `IfcBasePoint` place the IFC at its real
coordinates. The geometry itself is always written as modelled:

- `site` - the offset goes on the IfcSite placement.
- `mapconversion` - adds `IfcMapConversion` + `IfcProjectedCRS` (Eastings/Northings
  in metres); needs `IfcCRS`, otherwise `site` is used.
- `world` - the vector is ignored.

```
IfcProject = "E14 Mindre betongkonstruksjoner"
IfcBasePoint = (98200000, 1609000000)
IfcBasePointExport = mapconversion
IfcCRS = "EPSG:5111"
```

IfcExport shows a warning when the geometry lies more than 1 km from the Rhino
origin: such large coordinates may display wrongly in IFC viewers.

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
