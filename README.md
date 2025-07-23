
# csv-Generator – Support Tool for TagTool_WiZArd

The tool is used for the structured recording of metadata and authority data, which can then be output as CSV files. It simplifies the creation of CSV tables required by the Word pre-structuring tool [TagTool_WiZArd](https://github.com/pBxr/TagTool_WiZArd). It allows users to enter relevant data into structured fields and automatically exports the content in the correct CSV format, using the required delimiter (`|`). The tool was created with the help of GPT-based code generation and drafting.

## Features Overview

- Structured entry of places, persons, references, illustration captions, and illustration credits
- Automatic CSV export
- Leading whitespace is automatically removed from entries
- ORCID validation via API
- Gazetteer integration (iDAI.gazetteer API) for place validation and Gazetteer-ID retrieval
- Interactive map view to assist with place selection
- Backend support for named entity recognition (NER) in `.docx` files (beta)

## HTML Module Overview

### 0. `index.html` – Start Page

The central entry point of the application. It provides an overview of all available modules via buttons and links. It also displays the institutional logo (DAI) and footer versioning information.

- Navigation to:
  - `01_MetadataValueList` (`metadata.html`)
  - `02_AuthorYearList` (`authoryear.html`)
  - `03_IllustrationCreditList` (`illustration.html`)
  - `04_ToSearchAndReplaceList` (`search_replace.html`)
  - `05_Place_Name_Extraction_via_NER` (`gazetteer_NER.html`) – **requires local server**
- Includes the DAI logo (`Deutsches_Archaeologisches_Institut_Logo.svg`) displayed from the same folder.

### 1. MetadataValueList (metadata.html)
This module allows you to enter article and author metadata. The tool checks the validity of the entered ORCID iDs using the ORCID public API.

### 2. AuthorYearList (authoryear.html)
This module helps to create standardized `Author+Year` citations and bibliography entries, including optional links to Zenon bibliographic IDs.

- This CSV enables TagTool_WiZArd to correctly format citation abbreviations and bibliographic references.
- If a Zenon ID is provided, TagTool will generate a clickable link to the bibliographic entry.

### 3. IllustrationCreditList (illustration.html)
This module helps to organize figure references, including their captions and source information.

- Input: e.g., `Fig. 3 | "View of the excavation" | © DAI`
- Output: A structured CSV that allows TagTool_WiZArd to insert correctly formatted image credits and captions.

### 4. ToSearchAndReplaceList (search_replace.html)
This module enables users to look up geographical names via the iDAI.gazetteer API and export Gazetteer-IDs.

- Input: Free-text place name (e.g., `Alexandria`)
- The tool queries the API and displays all matches with types and coordinates.
- A Leaflet map helps to visually identify the correct location.
- Once selected, the correct iDAI.gazetteer URI is placed into the table for CSV export.

### 5. Place_Name_Extraction_via_NER (gazetteer_NER.html) – requires local server (see below "Backend")

This module allows users to upload .docx files, extract place names via Named Entity Recognition (NER), and match them against the iDAI.gazetteer API. A local Python server with spaCy must be running for this to work. Results are displayed with possible matches and coordinates on an interactive map.

## Backend (Flask + spaCy)

- A small Python Flask server enables `.docx` file upload and text analysis.
- Named Entity Recognition (NER) for places is performed using spaCy (`de_core_news_lg`).
- The backend parses paragraphs and tables from `.docx` documents.
- **Note:** The NER component is still in **beta** and may not provide reliable results (This is a small model that is also designed for German-language text.).

## Creator

The code and README file were generated and structured with ChatGPT.
