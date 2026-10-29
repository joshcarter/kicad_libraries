# JDC KiCad Libraries

Personal KiCad symbol, footprint, and 3D model libraries.

## Layout

```
symbols/      JDC_<Category>.kicad_sym
footprints/   JDC_<Category>.pretty/<Vendor>_<PartNo>.kicad_mod
3dmodels/     JDC_<Category>.3dshapes/<Vendor>_<PartNo>.step
```

| Library | Contents |
|---|---|
| `JDC_MCU` | Raspberry Pi CM5, Raspberry Pi Pico |
| `JDC_Connectors` | TE 770149-1, Keystone 5019 test point |

Parts are named `<Vendor>_<PartNo>`, using the vendor's exact part number.

## Setup

1. In KiCad, open **Preferences → Configure Paths** and add:

   | Name | Path |
   |---|---|
   | `JDC_KICAD_LIB` | path to this repository |

   Footprints find their 3D models through
   `${JDC_KICAD_LIB}/3dmodels/...`, so this works on any machine.

2. Add the libraries under **Preferences → Manage Symbol Libraries** and
   **Manage Footprint Libraries**, or paste these into the global
   `sym-lib-table` / `fp-lib-table`:

   ```
   (lib (name "JDC_MCU")(type "KiCad")(uri "${JDC_KICAD_LIB}/symbols/JDC_MCU.kicad_sym")(options "")(descr ""))
   (lib (name "JDC_Connectors")(type "KiCad")(uri "${JDC_KICAD_LIB}/symbols/JDC_Connectors.kicad_sym")(options "")(descr ""))
   ```

   ```
   (lib (name "JDC_MCU")(type "KiCad")(uri "${JDC_KICAD_LIB}/footprints/JDC_MCU.pretty")(options "")(descr ""))
   (lib (name "JDC_Connectors")(type "KiCad")(uri "${JDC_KICAD_LIB}/footprints/JDC_Connectors.pretty")(options "")(descr ""))
   ```

## Adding a part

- Put it in an existing category library where possible; add a new
  `JDC_<Category>` only when nothing fits.
- Name the symbol, footprint, and 3D model `<Vendor>_<PartNo>`.
- Set the symbol's `Footprint` field to `JDC_<Category>:<Vendor>_<PartNo>`.
- Reference 3D models as `${JDC_KICAD_LIB}/3dmodels/JDC_<Category>.3dshapes/<file>`,
  never an absolute path.
