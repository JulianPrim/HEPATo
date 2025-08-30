
# HEPATo (HepG2 Promoter Analysis Tool)
An interactive R Shiny viewer for HepG2 cells that overlays ENCODE cCREs with ChIP-Atlas transcription factors, histone marks, and ATAC-seq around any HGNC gene to guide regulatory network studies in liver cancer.


---------------------------------------------------------------------------------------
## How to run the viewer locally

Go to the project’s GitHub → click on "Releases" and download the three pre-formatted ChIP-Atlas and the ENCODE cCREs bed files.
Place them in the same folder as your app (expected names):
HepG2_formatted_50_AllAg.bed, HepG2_formatted_50_His.bed, HepG2_formatted_50_ATAC.bed, and the cCRE bigBed.

In RStudio: File → New File → Shiny Web App… (single-file app).
Name it as you like and create it.

Replace the template with the app code (the “Raw_codeV2.0.0”) and save as app.R in that folder.

Install the required packages mentioned at the top of the script, then to run it click on "Run App"

Or run the script line-by-line (Command+Enter for mac).

If the Run App button is buggy on your setup, use shiny::runApp(".") instead.

Enjoy it !
---------------------------------------------------------------------------------------
<img width="1468" height="893" alt="image" src="https://github.com/user-attachments/assets/5e51c308-cea9-40ef-b48e-de037f776258" />
<img width="1421" height="755" alt="Capture d’écran 2025-08-28 à 14 22 32" src="https://github.com/user-attachments/assets/50c3f209-c69f-4919-8fce-5f9b0b4f252f" />
<img width="935" height="246" alt="image" src="https://github.com/user-attachments/assets/5d73ab66-cde9-4035-a090-8fe9a80cc092" />

The legend is not exhaustive



## Author     : Julian Primig (Sorbonne Université)
Date        : 2025-08-27,
Requirements: R (>=4.2), Bioconductor packages (EnsDb.Hsapiens.v86, etc.)
Made with   : R 4.5.1, ChatGPT 5 (used for code syntax and development)

## Data sources:
   - ENCODE Registry of cCREs (hg38), file ENCFF389ZVZ.bigBed, lab: Zhiping Weng, UMass
   - ChIP-Atlas Peak Browser (https://chip-atlas.org) Accessed: 2025-07
   -  Dataset type: ChIP-seq (TFs, histone marks), ATAC-seq
   - Reference: Oki et al., Nucleic Acids Research 2024 (doi:10.1093/nar/gkae358)


## Notes & data format

> **ChIP-Atlas is continuously updated.** Analyses here reflect the snapshot listed above (accessed **July-2025**).

All peak tracks use a **uniform 6-column BED-like schema**:


- `chrom`, `start`, `end` — genomic interval (hg38)  
- `SRX` — SRA experiment accession from ChIP-Atlas  
- `gene` — assayed factor/mark (e.g., TF name or histone modification)  
- `score` — peak score reported by the source

## Included HepG2 datasets

| File                           | Track                                  | SRX datasets |
|--------------------------------|----------------------------------------|--------------|
| `HepG2_formatted_50_AllAg.bed` | ChIP-Atlas **TFs** (antibodies to TFs) | **1766**     |
| `HepG2_formatted_50_His.bed`   | ChIP-Atlas **histone marks**           | **172**      |
| `HepG2_formatted_50_ATAC.bed`  | **ATAC-seq** peaks/scores              | **50**       |

## Usage

Place these files **next to** `app.R`.  
The app will load the file that matches the selected **track** and overlay those peaks with **ENCODE cCREs** around the requested **HGNC** gene.

> SRX counts reflect the July-2025 ChIP-Atlas snapshot and may change as the resource updates.


