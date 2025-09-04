
# HEPATo (HepG2 Promoter Analysis Tool)
An interactive R Shiny viewer for HepG2 cells that combines ENCODE candidate Cis Regulatory Elements (cCREs) with ChIP-Atlas transcription factors, histone marks, and ATAC-seq data within currently annotated HGNC genes to facilitate exploring regulatory networks in liver cancer cells and to easily produce elegant ChIP-seq figures. This tool is meant to help generate hypotheses or confirm existing results. 


---------------------------------------------------------------------------------------
## How to run the viewer locally

1. In RStudio (not R), click on File -> New File -> Shiny Web App… (single-file app).
Name it as you like (HEPATo) and create it. This will create a folder on your device with the name you chose. 

<img width="252" height="100" alt="image" src="https://github.com/user-attachments/assets/b9322cd5-da8e-4139-95ef-5a5e43106675" />

2. Go to the project’s GitHub page -> click on "Releases" and download the three pre-formatted ChIP-Atlas and the ENCODE cCREs bed files.
Place them in the same folder as your app (expected names):
HepG2_formatted_50_AllAg.bed, HepG2_formatted_50_His.bed, HepG2_formatted_50_ATAC.bed, and the cCRE bigBed.

<img width="428" height="118" alt="image" src="https://github.com/user-attachments/assets/8aa8bf2e-f616-4f9d-90ce-4dca55a0cd64" />

3. In RStudio, session -> set working directory -> choose directory -> select the folder
   
4. Replace (copy-paste) the template in the Rstudio script with the app code (the “RawCode_v.1.0.0”) and save as app.R in that folder.

The script starts by installing packages. Use the viewer once (click Run App). Then, for later uses, inactivate the packages installation code block, by putting hashtags (#) in front of the lines to prevent reinstalling packages. Just press Run app again.

<img width="612" height="114" alt="image" src="https://github.com/user-attachments/assets/9ca4b71c-f209-465d-9cbe-d946611a0dbf" />

In case Run app fails to execute properly, you can run the script line by line from the beginning (maintain Command+Enter for mac).

If you use this viewer, please read the notes of caution below.
---------------------------------------------------------------------------------------
<img width="1467" height="897" alt="image" src="https://github.com/user-attachments/assets/2655095b-f849-4a08-bf5b-d3729f899f78" />

<img width="864" height="669" alt="image" src="https://github.com/user-attachments/assets/149685f8-233e-4776-87e2-71f4cb8b31c2" />

<img width="783" height="244" alt="image" src="https://github.com/user-attachments/assets/ff1ccd50-d510-44b9-8150-c19171457e22" />


The legend is not exhaustive here



## Author: Julian Primig (Sorbonne Université)
Date        : 2025-08-27,
Requirements: R (>=4.2), Bioconductor packages (EnsDb.Hsapiens.v86, etc.)
Made with   : R 4.5.1, ChatGPT 5 (used for code syntax and development)

## Data sources
   - ENCODE Registry of cCREs (hg38), file ENCFF389ZVZ.bigBed, lab: Zhiping Weng, UMass
   - ChIP-Atlas Peak Browser (https://chip-atlas.org) Accessed: 2025-07
   -  Dataset type: ChIP-seq (TFs, histone marks), ATAC-seq
   - Reference: Oki et al., Nucleic Acids Research 2024 (doi:10.1093/nar/gkae358)


## Data format

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

# Notes of caution

The error "subscript out of bound" in the legend occurs when the user selects less than three TFs. 


### HEPATo plots peaks midpoint
In the graphical output, points are placed at the center of each ChIP-seq signal rather than the peak, since the ChIP-Atlas BED files used here don’t provide the exact peak positions. consequently, the x-coordinate is informative for regional localization but not precise enough for base-pair alignment to exact predicted binding sites. Overlapping peaks can have different genomic lengths. Since positions are drawn at the peak midpoint, they won’t coincide exactly when you zoom in. We recommend verifying the genomic coordinates for any TF binding signal of interest.

<img width="333" height="280" alt="image" src="https://github.com/user-attachments/assets/cd40c5b4-2dff-42e0-a394-27b90f45a362" />



### MACS2 scores are not comparable accros studies 
The score column in Peak Browser BEDs is the MACS2 display score (–10·log10 q-value, capped ~0–1000) in BED9 field 5. It’s a ranking/visualization aid not a raw MACS2 statistic (qValue/pValue/signalValue) for cross-study quantitation. Use it only for within-study (same SRX) peak ranking; do not compare across SRXs.

### Hotspot promoters can yield false positive 
Please note that hotspot promoters highly transcribed and accessible are prone to “phantom peaks” arising from biochemical artefacts. Even though the data are from wet lab experiments, they should be considered exploratory leads for cancer regulatory network research. For references See PMIDs: 31114922, 24173036, 26117547.

 
