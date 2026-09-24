# TI-84 Evo / Plus CE List Converter

A single-page, browser-based editor and converter for TI calculator real-number list files.

<img width="680" alt="image" src="https://github.com/user-attachments/assets/6d76c74a-8686-4e01-b570-51ff5682b586" />

The app can import **TI-84 Plus CE `.8xl`** list files and **TI-84 Evo `.8xl2`** list files, display the values in editable columns, and export each list in either format.

All conversion and editing happens locally in the browser. No files are uploaded to a server.

Link to live app: https://realityexpander.github.io/TI-84-Evo-Plus-CE-List-Converter/

## Features

- Import TI-84 Plus CE real-number lists in `.8xl` format.
- Import TI-84 Evo real-number lists in `.8xl2` format.
- Load up to six lists into **List 1** through **List 6**.
- Automatically use the loaded filename, without the extension, as the editable list header.
- Edit list values directly in the browser.
- Supports integers, decimal values, and scientific notation such as `1.25e-6`.
- Press **Enter** in a value field to insert a new row directly below it containing `0`; the new `0` is automatically selected and ready to replace by typing.
- Add new values to any list with **+ Add value**.
- Hover over a value field to reveal a **Ⓧ** control for deleting that item from that list only.
- Clear an individual list after confirmation.
- Clear all six lists at once with **Clear All**, after confirmation.
- Load a file directly into a specific list with that list's **Load .8xl\*** button.
  - Accepts either `.8xl` or `.8xl2`.
  - The selected file is loaded into that exact list regardless of its filename or internal list name.
- Drag and drop a `.8xl` or `.8xl2` file directly onto any list header.
  - Each editable list name is surrounded by a dashed border to identify it as a drop target.
  - The target highlights while a file is dragged over it.
  - The dropped file is loaded into that exact list, replacing any existing data there.
- Drag and drop multiple `.8xl` and/or `.8xl2` files onto the top **Drag & Drop Here to Import All** target.
  - Imports up to the first six dropped files.
  - Mixed `.8xl` and `.8xl2` files can be dropped together.
  - Uses the same automatic placement behavior as the top **Load List(s)** controls.
- Export a single list as:
  - `.8xl`
  - `.8xl2`
- Export all populated lists at once as separate:
  - `.8xl` files
  - `.8xl2` files
- Editable list headers determine the downloaded filename.
- Preserves a valid TI list variable name when possible for the calculator's internal list name.
- Performs checksum validation when importing supported files.
- Runs entirely as a single HTML file with no installation required.
- Link to conversation with ChatGPT 5.6 Sol on High: https://chatgpt.com/share/6ab477f0-b560-83ea-9e50-590ea0bf7d30

## Supported Calculators and Formats

| Calculator | List format | Extension |
| --- | --- | --- |
| TI-84 Plus CE and compatible TI-83/84 family list files | Real-number list | `.8xl` |
| TI-84 Evo | Real-number list | `.8xl2` |

The application is intended for **real-number lists**. Complex-number lists and unsupported Evo expression types are outside the current scope.

## Using the App

### Load several lists

Use either button at the top of the page:

- **Load List(s) — .8xl**
- **Load List(s) — .8xl2**

You can select multiple files. The app uses up to the first six selected files and places them into available lists.

### Drag and drop several lists at once

Next to the top **Load List(s)** buttons is a dashed drop target labeled:

**Drag & Drop Here to Import All**

You can drag multiple `.8xl` and/or `.8xl2` files onto this target. The app imports up to the first six files and places them using the same automatic placement behavior as the bulk file-picker buttons.

### Load a file into a specific list

Each list has a **Load .8xl\*** button.

1. Click **Load .8xl\*** under the desired list.
2. Select either a `.8xl` or `.8xl2` file.
3. The file is loaded directly into that list.
4. Existing data in that list is replaced.

This is useful when the filename does not correspond to the desired L1-L6 list.

### Drag and drop a file into a specific list

Each editable list header also acts as a drag-and-drop target. The dashed border around the list name indicates the active drop area.

1. Drag a `.8xl` or `.8xl2` file from your computer.
2. Move it over the desired list name.
3. The drop target highlights while the file is over that list.
4. Drop the file to load it directly into that list.
5. Existing data in that list is replaced.

The file is loaded into the selected list regardless of the filename or internal TI list name.

### Edit a list

Each number is shown in an editable field. Values may be entered as:

```text
0
42
-18
0.001
-12.5
1.25e-6
3.2E8
```

You can add values in either of two ways:

- Press **Enter** while editing a value. A new row is inserted directly below with `0`, and that `0` is automatically highlighted so you can immediately type the next value.
- Click **+ Add value** at the bottom of the list.

### Delete an individual value

Hover over any value field to reveal a **Ⓧ** icon on its right side. Clicking **Ⓧ** asks for confirmation before deleting only that item from that list.

### Clear lists

Each list has a **Clear** button. The top toolbar also has **Clear All**, which clears all six lists at once.

All destructive actions use the same confirmation dialog:

- **No** appears on the left.
- **Yes** appears on the right and is highlighted/focused by default.
- Press **Y** or **Enter** for **Yes**.
- Press **N** or **Esc** for **No**.

### Rename an exported file

The header above each list is editable. The text in that header is used as the base filename when downloading that list.

For example, changing a header to:

```text
TESTDATA
```

and clicking **Save .8xl2** downloads:

```text
TESTDATA.8xl2
```

The calculator's internal list-variable name is kept separate from the download filename. If the edited header is itself a valid TI list name, the app can use it as the internal list name; otherwise it preserves the imported internal name or the list's default L1-L6 name.

### Export one list

Each list provides:

- **Save .8xl**
- **Save .8xl2**

These buttons convert and download only that list.

### Export all lists

At the top of the page:

- **Export all as .8xl**
- **Export all as .8xl2**

Each populated list is downloaded as a separate file. Some browsers may ask for permission to allow multiple downloads.

## Technical Notes

### TI-84 Plus CE `.8xl`

The app reads and writes the standard TI-83/84-family variable-file container used for real-number lists. Numeric entries use the calculator's 9-byte BCD real-number representation with up to 14 significant decimal digits.

### TI-84 Evo `.8xl2`

TI-84 Evo list files use a different container and numeric representation from legacy `.8xl` files. The app handles the Evo CBOR-based container, list metadata, numeric-expression data, and Evo checksum used by supported real-number lists.

The Evo implementation was developed with reference to the open-source `tivars_lib_cpp` project:

https://github.com/adriweb/tivars_lib_cpp

`tivars_lib_cpp` is distributed under the MIT License. Attribution for the referenced implementation is also included in the HTML source.

## Running Locally

No build process or web server is required.

1. Download or clone this repository.
2. Open `ti84_list_editor.html` in a modern browser.
3. Load your calculator list files.
4. Edit or convert them as needed.

Because the application is entirely client-side, it can also be used offline after the HTML file has been downloaded.

## Browser Compatibility

The app uses standard modern browser APIs including:

- `FileReader` / file input handling
- HTML5 drag-and-drop events for per-list and bulk file loading
- `Uint8Array`
- `Blob`
- browser-generated downloads

A current version of Chrome, Edge, Firefox, or Safari is recommended.

## Privacy

Calculator files are processed locally inside the browser tab. The application does not upload list data to a remote service.

## Limitations

- Designed for real-number lists.
- Complex-number list data is not currently supported.
- Some unsupported TI-84 Evo expression types may be rejected during import.
- The application converts numeric values; textual display formatting from the original calculator file is not necessarily preserved because the file stores numeric data rather than the exact text originally typed.
- Browsers can require explicit permission when the **Export all** commands trigger several downloads.

## Repository

Source code:

https://github.com/realityexpander/TI-84-Evo-Plus-CE-List-Converter

## Copyright

©2026 Chris Athanas
