# make3 Makefile
path= ./graphics/
pdfs= $(path)lm1.pdf $(path)lm1_spline.pdf $(path)lm2.pdf
# --------------------------------------------------------------

all: $(pdfs)

mtcars_red.RData: createdata.R
	R CMD BATCH --no-save createdata.R
	
results.RData: makeanalysis.R mtcars_red.RData
	R CMD BATCH --no-save makeanalysis.R


## ---- MULTIPLE TARGETS -----------
$(pdfs): creategraphics_inter

.SECONDARY: creategraphics_inter

creategraphics_inter: creategraphics.R results.RData
	R CMD BATCH --no-save creategraphics.R
## ---------------------------------

# das ist die unelegante Moeglichkeit die Abhaengigkeiten zu bestimmen
# weil das .Rout auch ertzeugt wird wenn ein Error passiert
# daher ist das wahrscheinlich eher nicht zu empfehlen
#creategraphics.Rout: creategraphics.R results.RData
#	R CMD BATCH --no-save creategraphics.R
	
# -------------------------------------------------------	

# wenn ein minus davor steht wird der error irgnored
clean:
	-rm *.Rout *.bak
	
clean_all:
	-rm *.Rout *.RData *.bak