# IfcGH - IFC 4.3 export for Grasshopper

Grasshopper components for **Rhino 8** that export Rhino geometry and
reinforcement (rebar groups) to **IFC 4.3** files, built on
[ifcopenshell](https://ifcopenshell.org/). Property sets follow the SNACks or
bruBIM (Statens vegvesen) property definitions.

This repository only hosts releases and user documentation.

## Install

Download the `.yak` from [Releases](../../releases) and follow
[docs/install.md](docs/install.md).

## Licence and data

- [MIT](LICENSE).
- The package includes property definitions derived from bruBIM (Statens
  vegvesen) and SNACks, and the `pybvbs` BVBS helper library.
- Third-party libraries (`ifcopenshell`, `openpyxl`) are downloaded from PyPI
  on first use under their own licences.
