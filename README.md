
# csv-Generator – Support Tool for TagTool_WiZArd

The tool is used for the structured recording of metadata and authority data, which can then be output as CSV files. It simplifies the creation of CSV tables required by the Word pre-structuring tool [TagTool_WiZArd](https://github.com/pBxr/TagTool_WiZArd). It allows users to enter relevant data into structured fields and automatically exports the content in the correct CSV format, using the required delimiter (`|`). The tool was created with the help of GPT-based code generation and drafting.

## Features Overview

- Structured entry of places, persons, references, illustration captions, and illustration credits
- Automatic CSV export
- Leading whitespace is automatically removed from entries
- ORCID validation via API
- Gazetteer integration (iDAI.gazetteer API) for place validation and URI retrieval
- Interactive map view to assist with place selection
- Backend support for named entity recognition (NER) in `.docx` files (beta)

## HTML Module Overview

### 1. Metadata (with ORCID check)
This module allows you to enter article and author metadata. The tool checks the validity of the entered ORCID iDs using the ORCID public API. The resulting CSV can be used by TagTool_WiZArd to match metadata to contributions.

### 2. Author + Year (Literature Abbreviations and Bibliography)
This module helps to create standardized `Author Year` citations and bibliography entries, including optional links to Zenon bibliographic IDs.

- This CSV enables TagTool_WiZArd to correctly format citation abbreviations and bibliographic references.
- If a Zenon ID is provided, TagTool will generate a clickable link to the bibliographic entry.

### 3. Illustrations / Captions
This module helps to organize figure references, including their captions and source information.

- Input: e.g., `Fig. 3 | "View of the excavation" | © DAI`
- Output: A structured CSV that allows TagTool_WiZArd to insert correctly formatted image credits and captions.

### 4. ToSearchAndReplaceList (Gazetteer + Map)
This module enables users to look up geographical names via the iDAI.gazetteer API and export place-URI mappings.

- Input: Free-text place name (e.g., `Alexandria`)
- The tool queries the API and displays all matches with types and coordinates.
- A Leaflet map helps to visually identify the correct location.
- Once selected, the correct iDAI.gazetteer URI is placed into the table for CSV export.

## Backend (Flask + spaCy)

- A small Python Flask server enables `.docx` file upload and text analysis.
- Named Entity Recognition (NER) for places is performed using spaCy (`de_core_news_lg`).
- The backend parses paragraphs and tables from `.docx` documents.
- **Note:** The NER component is still in **beta** and may not provide reliable results (This is a small model that is also designed for German-language text.).

## Creator

The code and README file were generated and structured with ChatGPT.
