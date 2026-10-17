# TI-84 Plus CE Lists ◀▶ Evo Lists

A browser-based **TI-84 Plus CE ↔ TI-84 Evo real-number list editor, converter, and USB transfer utility**. Import list files, retrieve lists directly from a connected calculator, edit their values, export to either calculator's file format, or send lists back to a connected calculator.

<img width="600" alt="TI-84 Plus CE and Evo list editor" src="https://github.com/user-attachments/assets/12cbb662-b37b-409e-9288-800e152c087d" />

- **Live app:** https://realityexpander.github.io/TI-84-Evo-Plus-CE-List-Converter/
- **Step-by-step conversion instructions using files (Not required with Latest Version):** https://realityexpander.github.io/TI-84-Evo-Plus-CE-List-Converter/Convert-TI-84-Plus-CE-To-Evo-Instructions/
- **Source repository:** https://github.com/realityexpander/TI-84-Evo-Plus-CE-List-Converter

**Current documented application version: 1.0v18.** File conversion and USB transfers run locally in your browser; calculator list data is not uploaded to a server.

## Features

### Import and export files

- Open TI-84 Plus CE `.8xl` and TI-84 Evo `.8xl2` **real-number list files**, including multiple files at once.
- Convert any list to either format using **Save .8xl** or **Save .8xl2**.
- Export all populated lists as separate `.8xl` or `.8xl2` files.
- Import mixed `.8xl` and `.8xl2` files by dragging them onto **Drag & Drop Here to Import All**.
- Drop a file onto an individual column's dashed filename field to load it into that column.
- Validate file checksums and warn when a checksum does not match. Readable data may still load with a warning.

### Connect directly to calculators

- **Get Plus CE Device Lists — WebUSB:** Read populated standard real-number lists **L1–L11** from a connected TI-84 Plus CE; skip empty lists and ignore unrelated variable types.
- **Get Evo Device Lists — WebUSB:** Read populated standard real-number lists **L1–L6** from a connected TI-84 Evo; skip empty lists and ignore nonstandard lists.
- **Send to Plus CE as Lx:** Send an editor column to the corresponding Plus CE destination list; the number **x** is the **editor column number**, not its editable filename.
- **Send L1 to Lx to Plus CE — WebUSB:** Send all populated editor columns to their corresponding Plus CE list numbers, skipping empty columns. The button displays the highest populated column as **x**.
- **Send to Evo as Lx:** Send a single one of the first six editor columns to the corresponding Evo list **L1–L6**.
- **Send L1 to L6 to Evo — WebUSB:** Send all populated editor columns among **L1–L6**, skipping empty columns.
- Check the destination calculator's directory before sending, and request confirmation before replacing lists reported as populated.

**Important:** Direct Plus CE sending was added in v17. Its protocol implementation has passed simulated tests, but a successful write to a physical Plus CE had **not yet been confirmed** in this project's testing. Back up calculator data and verify a small test list before sending important lists or using the bulk-send command.

### Edit lists

- Show **six columns by default**, expanding automatically as needed to a maximum of **12 columns**.
- Edit integers, decimals, and scientific notation (for example, `1.25e-6`).
- Press **Enter** in a value field to insert a new row immediately below, with `0` selected for immediate editing.
- Use **+ Add value** to append a value, or hover over a row and click **Ⓧ** to delete that entry.
- Use **Drag To Copy** to copy one entire column to another column's dashed filename target.
- Edit the column header to control the filename of downloaded list files.
- Clear one column or all columns, each with a confirmation dialog.

## Supported Calculators and Formats

| Calculator | File format | Direct device import | Direct device send |
| --- | --- | --- | --- |
| **TI-84 Plus CE** | `.8xl` | WebUSB; standard real lists **L1–L11** | WebUSB; corresponding editor-column list numbers, subject to device limits |
| **TI-84 Evo** | `.8xl2` | WebUSB; standard real lists **L1–L6** | WebUSB; standard real lists **L1–L6** |

Compatible TI-83/84-family `.8xl` *files* may also be opened for conversion; that does not mean the app has been tested for direct USB connections to every calculator in that family.

The app works with **real-number lists**. Complex lists and unsupported Evo expression types are outside its current scope. The Plus CE has a limit of **999 elements per list**, which the direct Plus CE sending code checks before beginning a transfer.

Although the editor can display 12 columns, that does **not** guarantee that a physical calculator supports all 12 corresponding built-in list names. In particular, Plus CE device import recognizes standard L1–L11; direct sending to an L12 destination has not been validated.

## Getting Started

### Use the live app

Open the [live app](https://realityexpander.github.io/TI-84-Evo-Plus-CE-List-Converter/) in a current desktop version of **Google Chrome or Microsoft Edge** for calculator USB operations. USB access requires browser permission; choose the correct calculator in Chrome's device chooser.

### Run locally on a Mac or PC

For file editing and conversion alone, you can open the HTML file in a browser. **For USB communication, use `http://localhost` rather than a `file://` URL.**

1. Download or clone the repository, and navigate to the directory containing the HTML application.
2. Make sure `favicon.ico` is in the same directory as the HTML file if you want the **84** browser-tab icon.
3. Start a local web server:

   ```bash
   python3 -m http.server 8000
   ```

4. Open `http://localhost:8000/` if your copy is named `index.html`, or open `http://localhost:8000/ti84_list_editor_usb_v18.html` if you are using the versioned file directly.
5. Connect your TI-84 Plus CE or TI-84 Evo using its USB data cable, then choose the appropriate **Get** or **Send** button.

No packages, build process, or backend application are required. The Python server delivers the static HTML; it does **not** receive or process calculator list data. After the page loads, all editing, conversion, and USB communication occur in the browser.

For USB access, the page needs a **secure context** (such as `https://` or `http://localhost`) and a Chromium-based browser supporting **WebUSB**. Evo initialization additionally uses **Web Serial**.

## Using the App

### 1. Load list files from your computer

Use either of these buttons:

- **Load List(s) — .8xl** for Plus CE-format files.
- **Load List(s) — .8xl2** for Evo-format files.

Select one or more files. You can also drag `.8xl` and `.8xl2` files together onto **Drag & Drop Here to Import All**. Up to **12 files** are considered per batch. The app prefers the matching standard list column when it is available; otherwise it uses an empty column.

For an exact destination, click a column's **Load .8xl\*** button (accepts both extensions), or drag a file onto that column's dashed filename field. This replaces the contents of that column regardless of the file's name.

### 2. Get lists directly from a Plus CE

1. Connect the TI-84 Plus CE to your computer with a USB data cable.
2. Click **Get Plus CE Device Lists — WebUSB**.
3. Select your calculator in the browser's WebUSB chooser and grant permission.
4. The app reads the device directory and imports populated standard real-number lists **L1–L11** into the editor.
5. Review the status bar for the count of lists imported, empty lists skipped, or any errors.

This **reads** calculator data; it does not erase or overwrite lists on the calculator.

### 3. Get lists directly from an Evo

1. Connect the TI-84 Evo to your computer with a USB data cable.
2. Click **Get Evo Device Lists — WebUSB**.
3. On first use, Chrome may ask you to authorize the Evo through **Web Serial** to initialize its USB CDC connection, and then ask separately for **WebUSB** access.
4. If Chrome requires a second user gesture for the WebUSB chooser, follow the app's message and click the same **Get Evo Device Lists — WebUSB** button again.
5. The app then imports populated standard **L1–L6** lists via **WebUSB**, skipping empty and nonstandard lists.

The automatic Web Serial open/close step is **initialization only**; list contents are retrieved through WebUSB. The app remembers successful initialization for that browser page session, so subsequent Evo WebUSB imports generally do not need to repeat it. There is no longer a separate **Get Evo Device Lists — Web Serial** button.

### 4. Edit and copy list values

Each numeric entry is editable. For example:

```text
0
42
-18
0.001
-12.5
1.25e-6
3.2E8
```

- **Enter:** Insert a new `0` row immediately below the current entry and select its value.
- **+ Add value:** Append a new `0` entry.
- **Ⓧ:** Delete one entry, with confirmation.
- **Drag To Copy:** Drag that button onto another column's dashed filename field to copy all values into the target column.

The dashed filename field is also editable. For example, changing a column heading to `TESTDATA` and pressing **Save .8xl2** downloads `TESTDATA.8xl2`.

The downloaded **filename** and the calculator's internal **list variable name** are distinct. For device sending, the destination is always determined by the editor column (`L1`, `L2`, etc.), even if the column's filename has been renamed.

### 5. Send one list to a Plus CE

**Back up existing calculator lists first, particularly while hardware write compatibility is being verified.**

1. Put a small test list into the editor column that matches the desired destination (for example, values `1`, `2`, `3` in editor **List 4**).
2. Click **Send to Plus CE as L4** under that column.
3. Select your Plus CE in the WebUSB chooser.
4. The app reads the calculator's directory and, if **L4** already contains data, asks **Confirm Overwrite Plus CE L4?**
5. Confirm to send, or select **No** to cancel.
6. Check the result on the calculator itself before transferring more data.

The app sends the list to the matching destination number, *not* to the filename shown in the editor header.

### 6. Send multiple lists to a Plus CE

1. Populate the editor columns you want to send.
2. Click **Send L1 to Lx to Plus CE — WebUSB**, where **x** is the highest populated editor column. When no columns contain data, the button reads **Send Lists to Plus CE — WebUSB**.
3. Select the Plus CE in the WebUSB chooser.
4. If destination lists already contain data, confirm the overwrite dialog; it identifies the populated destinations to be replaced.
5. The app transfers **only populated columns**, retaining their original destination numbers. For example, populated editor **L1, L3, and L6** are sent to **L1, L3, and L6**, respectively.
6. If the calculator does not acknowledge a write, the app **stops the batch** rather than attempting the remaining lists on a potentially unsynchronized USB connection.

The button is not a command to replace every intermediate list; empty editor columns are skipped.

### 7. Send lists to an Evo

To send a single populated column among **List 1–List 6**, click **Send to Evo as Lx** under that column. To send all populated columns in that range, click **Send L1 to L6 to Evo — WebUSB**.

1. Select your Evo in the WebUSB chooser.
2. The app reads its directory to find existing destination lists.
3. If one or more destinations already contain data, confirm the overwrite prompt.
4. The app sends each selected column to its matching Evo list **L1–L6**, not the editable filename.
5. Check the status message and calculator after the transfer.

Empty editor columns are skipped. The implementation attempts to retain the previous RAM/archive destination when available and may retry using archive memory for certain reported memory errors.

### 8. Export a single list or all lists

Each column has:

- **Save .8xl** — download a Plus CE-format list file.
- **Save .8xl2** — download an Evo-format list file.

The top toolbar has:

- **Export all as .8xl files**
- **Export all as .8xl2 files**

Exporting all produces a **separate download for each populated or loaded column**, rather than one combined file. Your browser may ask permission for multiple downloads.

### 9. Delete or clear data

- Hover over an individual value and click **Ⓧ** to remove that entry after confirmation.
- Click a column's **Clear** button to open **Confirm Clear List X?** for the selected column.
- Click the top **Clear All** button to open **Confirm Clear All Lists?**; this clears every editor column and resets the display to six columns.

In confirmation dialogs, **Y** or **Enter** means **Yes**, while **N** or **Esc** means **No**. The **Yes** button is focused by default, so review the action before pressing Enter.

## Technical Notes

### Plus CE `.8xl` format

The app reads and writes the TI-83/84-family variable-file container for supported real-number lists. Real values use **9-byte BCD** encoding with up to **14 significant decimal digits**.

For device transfers, the Plus CE uses the **TI DUSB** protocol over WebUSB. Before sending, the app checks the destination directory, then performs the request-to-send (**RTS**), variable-contents, and end-of-transfer (**EOT**) sequence with calculator acknowledgments.

### Evo `.8xl2` format

The Evo uses a different **CBOR-based container**, numeric-expression data representation, and checksum. The editor converts supported real-number data between `.8xl` and `.8xl2` formats.

Evo device transfers use **Kermit** over USB. On supported browsers and systems, the app first initializes the calculator's CDC connection through Web Serial (115200 baud) when needed, then performs list retrieval through WebUSB. Evo WebUSB sending is limited to **L1–L6**.

### Reference implementations

The format and transfer implementations were developed with reference to public/open-source TI calculator work, including:

- [`tivars_lib_cpp`](https://github.com/adriweb/tivars_lib_cpp) for TI variable file formats (MIT License).
- [`evo_usb_py`](https://github.com/Evo-Programming/evo_usb_py) and related TI/Kermit transfer documentation for Evo USB transfers.
- TI DUSB protocol references and [the open-source Plus CE sender](https://github.com/Redgale/TICAI-TI84-Cesium-Auto-Installer) for Plus CE device sending.

The relevant attribution and MIT license notice are included in the HTML application's source.

## Browser Compatibility

| Browser | Edit/convert local list files | Direct calculator USB operations |
| --- | --- | --- |
| Current desktop **Chrome** | Yes | **Recommended**; WebUSB and Web Serial support |
| Current desktop **Microsoft Edge** | Yes | Supported when WebUSB and Web Serial are available |
| **Firefox / Safari** | File editing/conversion may work | No direct USB support through the APIs required by this app |

If connecting fails:

1. Confirm that you are using a **USB data cable**, that the calculator is powered on, and that the correct device is selected.
2. Close TI Connect or any other application/tab that may be holding the calculator's USB interface.
3. If running locally, use `http://localhost:8000/` rather than opening the page as `file://`.
4. For the Evo, allow both Web Serial initialization and WebUSB permission when prompted; retry the **Get Evo Device Lists — WebUSB** button if requested.
5. Look at the app's status bar and Chrome DevTools → **Console** for connection or protocol errors.

## Privacy

The app processes file data and transfers calculator lists **locally in the browser**. The static website or local Python HTTP server delivers the HTML but is not used as an intermediary for calculator list transfers. USB access requires your explicit browser permission.

## Limitations and Precautions

- The application supports **real-number lists**, not complex-number lists or every calculator-specific expression type.
- File-format conversion preserves supported numeric values, but may not preserve the exact original text formatting used when values were entered on the calculator.
- The app displays up to **12 editor columns**, but Evo device operations target only **L1–L6**; Plus CE device import recognizes **L1–L11**.
- Direct Plus CE sending is implemented but, as of v18, **not yet verified on physical Plus CE hardware** in this project. Test with a disposable list and confirm the result on the calculator first.
- Sending to a calculator can **overwrite an existing populated destination list** after you confirm the prompt. Consider exporting a `.8xl`/`.8xl2` backup or using **Get Device Lists** first.
- Standard calculator limits apply, including **999 elements per Plus CE list**.
- Browsers may request separate Web Serial/WebUSB permissions or permission to download several files.

## Project and Development

- **Repository:** https://github.com/realityexpander/TI-84-Evo-Plus-CE-List-Converter
- **Development conversation:** https://chatgpt.com/share/6ab477f0-b560-83ea-9e50-590ea0bf7d30

## Copyright

©2026 Chris Athanas
