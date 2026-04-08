# DataMatrix VDA Generator

A static webpage for generating ISO 15434 compliant Data Matrix (ECC 200) codes for VDA labels.

## Usage

Open `index.html` in a browser (or serve it with any static file server).

Fill in any combination of the following fields and click **Generate Data Matrix Code**:

| Field | Prefix | Description |
|---|---|---|
| Part Number | `P` | Materialnummer |
| Revision | `2P` | Revision |
| Serial Number | `S` | Seriennummer |
| Supplier | `V` | Lieferant |
| Charge / Lot Number | `1T` | Charge |
| Ident Number | `1P` | Ident |
| Order Number | `K` | Bestellnummer |

## ISO 15434 Format

The generated code follows the structure:

```
[)>RS06GSP{matnr}GS2P{revision}GSS{serial}GSV{supplier}GS1T{charge}GS1P{ident}GSK{order}RSEOT
```

Special control characters used:

| Name | ASCII (Dec) | ASCII (Hex) |
|------|------------|-------------|
| GS   | 29         | 0x1D        |
| RS   | 30         | 0x1E        |
| EOT  | 4          | 0x04        |

## Dependencies

- [bwip-js](https://github.com/metafloor/bwip-js) — bundled locally (`bwip-js-min.js`), no internet connection required.
