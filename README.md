
# HepG2-ChIP-Viewer
An interactive R Shiny viewer for HepG2 cells that overlays ENCODE cCREs with ChIP-Atlas transcription factors, histone marks, and ATAC-seq around any HGNC gene to guide regulatory network studies in liver cancer.


---------------------------------------------------------------------------------------
How to run the viewer locally

Go to the project’s GitHub → click on "Releases" and download the four pre-formatted ChIP-Atlas files.
Place them in the same folder as your app (expected names):
HepG2_formatted_50_AllAg.bed, HepG2_formatted_50_His.bed, HepG2_formatted_50_ATAC.bed, and the cCRE bigBed.

In RStudio: File → New File → Shiny Web App… (single-file app).
Name it as you like and create it.

Replace the template with the app code (the “Raw code #2”) and save as app.R in that folder.

Install the required packages mentioned at the top of the script, then to run it, copy: shiny::runApp(".") ; in the board (console). 

Or run the script line-by-line (Shift+Enter).

If the Run App button is buggy on your setup, use shiny::runApp(".") instead.

Enjoy it !
---------------------------------------------------------------------------------------
<img width="1467" height="881" alt="image" src="https://github.com/user-attachments/assets/bacfd96a-7bb0-4546-a066-02da8c15d468" />
<img width="1421" height="755" alt="Capture d’écran 2025-08-28 à 14 22 32" src="https://github.com/user-attachments/assets/50c3f209-c69f-4919-8fce-5f9b0b4f252f" />
<img width="935" height="246" alt="image" src="https://github.com/user-attachments/assets/5d73ab66-cde9-4035-a090-8fe9a80cc092" />



# Author     : Julian Primig (Sorbonne Université)
Date        : 2025-08-27
Requirements: R (>=4.2), Bioconductor packages (EnsDb.Hsapiens.v86, etc.)
Made with   : R 4.5.1, ChatGPT 5

# Data sources:
   - ENCODE Registry of cCREs (hg38), file ENCFF389ZVZ.bigBed, lab: Zhiping Weng, UMass
   - ChIP-Atlas Peak Browser (https://chip-atlas.org) Accessed: 2025-07
   -  Dataset type: ChIP-seq (TFs, histone marks), ATAC-seq
   - Reference: Oki et al., Nucleic Acids Research 2024 (doi:10.1093/nar/gkae358)

# Notes:
#   ChIP-Atlas data are continuously updated; analyses correspond to the snapshot available on the access date above.
