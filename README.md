
# HepG2-ChIP-Viewer
An interactive R Shiny viewer for HepG2 cells (liver cancer) that overlays ENCODE cCREs with ChIP-Atlas transcription factors, histone marks, and ATAC-seq around any HGNC gene to guide regulatory network studies in liver cancer.


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
