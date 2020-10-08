Data for:
Roche DG, Kruuk LEB, Lanfear R, Binning SA (2015) Public data archiving in ecology and evolution: how well are we doing? PLOS Biology e1002295 doi:10.1371/journal.pbio.1002295
Data collected by DGR, SAB, AP and AA. Please refer to the manuscript for data collection methods and statistical analyses. For questions or to notify the authors if any errors are identified in the data, please contact Dominique Roche (dominique.roche@mail.mcgill.ca), Loeske Kruuk (loeske.kruuk@anu.edu.au), Rob Lanfear (rob.lanfear@gmail.com), or Sandra Binning (sandra.binning@mail.mcgill.ca).

These data were used for:
S2 Text. Interrater agreement analysis

### Inter-rater_analysis.csv ###

Colum heading	Description

rater		Letter (A, B, C or D) identifying the person rating the completeness and reusability of archived data.
dataset		Dataset number (0 to 100)
journal		Name of accompanying publication, taken from [1]
year		Year of publication, taken from [1]
embargoLgth	Taken from [1]. -1: no embargo (data released upon accession, at discretion of author); 0: no embargo (data released upon appearance of the accompanying publication online, default); 1: data released 1 yr following accompanying publication; etc.
dataType	What type of data are archived (e.g. measurements [meas] , observations [obs], genetic [gen], etc.)?
format		What format(s) are the data presented in (e.g., table, image, text, movie)?
noFiles		Number of files archived on Dryad (excluding the readme files).
fileExt		File extension.
fileExtReuse	Reusability potential of file format used. 0=low (proprietary and/or non-machine readable). 1=high (non-proprietary, machine-readable).
readme		Are the data descriptors in the readme file or the Dryad data description box complete (sufficient to make sense of the archived data without having to refer to the paper to understand the column headings, abbreviations and units)? 0 = incomplete, 1 = complete
analysisPgrm	Program(s) used for the statistical (or other) analyses.
analysisCode	Were the statictical analyses done using script/code or a GUI? 1= code, 2=GUI, NA=uncertain
codeArchived	Is the script/code for the analyses archived in a public repository or available as electronic supplementary material? 1=yes, 2=no
complScore	Score from 1 (poor) to 5 (exemplary) describing the completeness of the archived data and metadata (see Table 2 in the manuscript). 
reuseScore	Score from 1 (very poor) to 5 (exemplary) describing the reusability of the archived data (see Table 2 in the manuscript). The reuse score is adjusted for 'supMatt', i.e. one point was subtracted when data were included as supplementary material on the journal website, except when the reusability score was 1 to avoid zero values (see Methods). 
suppMat		Are some data included as electronic supplementary material that are not archived on Dryad? 1=yes, 2=no
notes		A summary of detailed notes taken for each study.

Columns not used for the analyses presented in the paper: dataType, format, noFiles, analysisPgrm, analysisCode, codeArchived
	
Abbreviations	Description

meas		measurements
obs		observations
gen		genetic
NA		for analysisPgrm = not applicable, for analysisCode = uncertain, for codeArchived = not applicable
some		for  codeArchived = some (but not all) code archived
	
	
References	
[1] Vision T, Scherle R, Mannheimer S (2013): Embargo selections of Dryad data authors. figshare. http://dx.doi.org/10.6084/m9.figshare.805946	
