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

## Validating a code

The **Validate a Data Matrix Code** section can read an existing code either with the
device camera (**Scan with camera**) or from an image file (**Select image file**).
The decoded content is checked against the ISO 15434 structure:

- start sequence `[)>` + RS + format indicator `06`
- end sequence RS + EOT
- GS separator between the header and each data segment, no empty segments
- syntactically valid data identifier prefixes (digits followed by one uppercase letter)
- no illegal control characters inside a segment, no duplicate data identifiers
- known VDA prefixes in the recommended order (deviations are reported as warnings)

The result is shown as a pass/fail verdict together with a detailed log listing every
error, warning and recognised segment.

## Dependencies

- [bwip-js](https://github.com/metafloor/bwip-js) — bundled locally (`bwip-js-min.js`), no internet connection required.
- [ZXing for JS](https://github.com/zxing-js/library) — bundled locally (`zxing-min.js`), used to decode Data Matrix codes for the validator.
