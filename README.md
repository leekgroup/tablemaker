# Tablemaker

## Installation
Precompiled binaries are available on Figshare:
* [OSX Binary](http://figshare.com/articles/Tablemaker_OS_X_Binary/1053136)
* [Linux Binary](http://figshare.com/articles/Tablemaker_Linux_Binary/1053137)

Alternatively, you can build tablemaker from source by following [these instructions](https://github.com/cole-trapnell-lab/cufflinks#building-cufflinks-from-source). (The process is the same as building Cufflinks from source). Source code is in the `tablemaker-2.1.1` directory.

*Note*: Tablemaker relies on Cufflinks version 2.1.1 (released April 2013) to estimate transcript FPKMs, and these estimates may not match FPKM estimates obtained from Cufflinks 2.2.0 (released March 2014) or 2.2.1 (released May 2014). We are actively working on integrating better with Cufflinks.

Please report any problems as issues on this repository. 

## Use
Users can run _Tablemaker_ to organize assembly output from the likes of _Cufflinks_ into a format that Ballgown can load.
                                                                                                     
Tablemaker needs to be run on each RNA-seq sample in your experiment.  It requires one single transcriptome assembly in [GTF format](http://www.ensembl.org/info/website/upload/gff.html) for a single experiment containing multiple samples.  _Tablemaker_ also requires read alignments for each sample in BAM format. From the command line, _Tablemaker_ is run as follows:
                                                                                                                          
`tablemaker -p 4 -q -W -G merged.gtf -o sample01_output sample_01/accepted_hits.bam`
                                                                                                                          
where:
* `-p` denotes how many threads to use (the program can take a few hours to run, but can be parallelized)
* The `-q` can be removed for more verbose output messages  
* `-W` and `-G merged.gtf` are required.  The `-W` tells the program to run in tablemaker mode (rather than Cufflinks mode), and the `-G` argument points to the assembly GTF file, which gives the assembled transcripts' structures. For Cufflinks users, often this is the `merged.gtf` output from [_Cuffmerge_](http://cole-trapnell-lab.github.io/cufflinks/cuffmerge/index.html).
* The argument to `-o` is the desired output directory for the sample (each sample should have its own output directory)
* The read alignment file is the last argument.  If reads were aligned with TopHat, this is usually some variant of `accepted_hits.bam`
