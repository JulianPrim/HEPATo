
# HEPATo (HepG2 Promoter Analysis Tool)
An interactive R Shiny viewer for HepG2 cells that combines ENCODE candidate Cis Regulatory Elements (cCREs) with ChIP-Atlas transcription factors, histone marks, and ATAC-seq data within currently annotated HGNC gene to facilitate exploring regulatory network in liver cancer cells.


---------------------------------------------------------------------------------------
## How to run the viewer locally

In RStudio (not R), click on File -> New File -> Shiny Web App… (single-file app).
Name it as you like (HEPATo) and create it. This will create a folder on your device with the name you chose. 

<img width="504" height="200" alt="image" src="https://github.com/user-attachments/assets/b9322cd5-da8e-4139-95ef-5a5e43106675" />

Go to the project’s GitHub page -> click on "Releases" and download the three pre-formatted ChIP-Atlas and the ENCODE cCREs bed files.
Place them in the same folder as your app (expected names):
HepG2_formatted_50_AllAg.bed, HepG2_formatted_50_His.bed, HepG2_formatted_50_ATAC.bed, and the cCRE bigBed.

<img width="428" height="118" alt="image" src="https://github.com/user-attachments/assets/8aa8bf2e-f616-4f9d-90ce-4dca55a0cd64" />

Replace (copy-paste) the template in the Rstudio script with the app code (the “Raw_codeV2.0.0”) and save as app.R in that folder.

The script starts by installing packages. Use the viewer once (click Run App). Then, for later uses, inactivate the packages installation code block, by putting hashtags (#) in front of the lines to prevent reinstalling packages. Just press Run app again.

<img width="612" height="114" alt="image" src="https://github.com/user-attachments/assets/9ca4b71c-f209-465d-9cbe-d946611a0dbf" />

In case Run app fails to execute properly , you run the script line by line from the beginning (maintain Command+Enter for mac).

If you use this viewer, please read the notes at the end.
---------------------------------------------------------------------------------------
<img width="1468" height="893" alt="image" src="https://github.com/user-attachments/assets/5e51c308-cea9-40ef-b48e-de037f776258" />
<img width="1421" height="755" alt="Capture d’écran 2025-08-28 à 14 22 32" src="https://github.com/user-attachments/assets/50c3f209-c69f-4919-8fce-5f9b0b4f252f" />
<img width="935" height="246" alt="image" src="https://github.com/user-attachments/assets/5d73ab66-cde9-4035-a090-8fe9a80cc092" />

The legend is not exhaustive here



## Author     : Julian Primig (Sorbonne Université)
Date        : 2025-08-27,
Requirements: R (>=4.2), Bioconductor packages (EnsDb.Hsapiens.v86, etc.)
Made with   : R 4.5.1, ChatGPT 5 (used for code syntax and development)

## Data sources:
   - ENCODE Registry of cCREs (hg38), file ENCFF389ZVZ.bigBed, lab: Zhiping Weng, UMass
   - ChIP-Atlas Peak Browser (https://chip-atlas.org) Accessed: 2025-07
   -  Dataset type: ChIP-seq (TFs, histone marks), ATAC-seq
   - Reference: Oki et al., Nucleic Acids Research 2024 (doi:10.1093/nar/gkae358)


## data format

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

## Notes of caution

The error "subscript out of bound" in the legend happens when the user selects less than 3 TFs. 

In this plot, points are placed at the center of each ChIP-seq peak rather than the summit, since the ChIP-Atlas BED files used here don’t provide summit positions. As a result, the x-coordinate is informative for regional localization but not precise enough for base-pair alignment to exact predicted binding sites. Overlapping peaks can have different genomic lengths. Since positions are drawn at the peak midpoint, they won’t coincide exactly when you zoom in. We recommend checking the genomic coordinates for any point of interest.

Hotspot promoters highly transcribed and accessible are prone to “phantom peaks” arising from biochemical artefacts. Even though the data are from wet lab experiments, they should be considered exploratory leads for cancer regulatory network research. 

Contact the corresponding author of the review for any questions, we're happy to answer. 
