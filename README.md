# G4Hunter multifasta seeker
#### Shiny App related to G4Hunter published in [Bedrat _et al._ NAR 2016][paper ref].  
Supplementary Data can be downloaded from [here](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4770238/bin/supp_44_4_1746__index.html).  
The _EF184640.1.fa_ file corresponds to the human mitochondrial genome used in the publication.  
The _hTERC.fa_ file corresponds to the human telomerase RNA component in RNA alphabet.  

> ##### The top part of this page allows you to compute the G4Hunter score of a single sequence. This main App (G4Hunter Seeker) identifies DNA or RNA regions in a longer sequence for which the G4Hunter score is above the chosen threshold in windows of the selected size. Please cite _"Bedrat A, Lacroix L, & Mergny JL (2016) Re-evaluation of G-quadruplex propensity with G4Hunter. Nucleic Acids Res 44(4):1746-1759."_, when reporting results obtained with this App.

##### The app requires the following packages:
* Biostrings
* GenomicRanges
* (S4Vectors)
* (shiny)

### Quick G4Hunter score
Just type your sequence in the box and you get the G4Hunter score below.  
Spaces are automaticaly removed, lower or upper cases are accepted.  
Characters orther than **G** or **C** are kept and counted as **A**,**T** or **U**.

###  G4Hunter multifasta seeker
Choose your multifasta file  (**Fasta File entry**).

Please notice that if the number of entries of your multifasta file is big (more than 100), the app will become **very slow**.

The **Threshold** and **Window size** determine the parameters for the sequence search as described in the [publication][paper ref].  
The higher the threshold, the more stringent the search: fewer G4 motifs wil be found, but these will be the most stable/likely ones.  


The file to download has to be a **DNA fasta** file that does not exceed the size limit imposed by Shiny (default is 5Mb, see below how to change it).  

The **Report sequences** option adds the nucleotide sequences in the output.  
The **Report G_sequences** option changes sequences with a negative score (C-rich sequences) into their reverse complement. Thus the output reports only G-rich sequences.

The **hits** report the number of sequences retrieved that match the settings.  
The **Number of the Input Sequence** corresponds to the number of entry in the multifasta file.

The output table contains the sequence name (**seqnames**), the **start**, **end** and **width** of the _refined_ sequences that meet the search criteria.  
The **strand** is **+** if the proposed G4 forming sequence is in the Input Sequence and this is set to **-** if the G4 forming sequence in on the reverse complementary strand.  
The **score** is the G4Hunter score of the _refined_ sequence and **max_score** is the highest score in absolute value in a window of the chosen **window size** for the sequence.  
**Threshold** and **window** are respectively the **Threshold** and **Window size** used for the search.  
The **sequence** corresponds to the _refined_ sequence in the **Input sequence**. This field is sensitive to the **Report G-sequences** option. This field is not present if the **Report sequences** option is not selected.  

> ##### Please note that the procedure extracts sequences that have a G4Hunter score above the threshold (in absolute value) in a window, fuses the overlapping sequences and then _refines_ theses sequences by removing bases at the extremities that are not G for sequences with a positive score (or C the negative ones). It also looks at the first neigboring base and adds it to the sequence if it is a G for sequences with a positive score (C for sequences with a negative score).  
> ##### Please see the [publication][paper ref] and Figure S1B for more details

The output can be exported to a text file that can be directly opened with _Microsoft Excel_.

--------------------------------------------------------------------------
As this is a simple Shiny app, there is a limit to the size you can upload (5Mb).  
If necessary (but might not be good for the host), the size limit can be increased  to XX Mb by adding the following code at the top of the server.R file (_adapted [from stackoverflow](http://stackoverflow.com/questions/18037737/how-to-change-maximum-upload-size-exceeded-restriction-in-shiny-and-save-user)_).  
```{r}
options(shiny.maxRequestSize=XX*1024^2)
```

--------------------------------------------------------------------------
_This project is independent of the [G4-Hunter python repository](https://github.com/AnimaTardeb/G4-Hunter) even if both project are related to the same [publication][paper ref]._


[paper ref]:http://doi.org/10.1093/nar/gkw006
