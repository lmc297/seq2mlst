# seq2mlst
## *In silico* multi-locus sequence typing (MLST) for bacterial genomes

## Overview

Perform *in silico* multi-locus sequence typing (MLST) using bacterial genomic data and the MLST schemes at PubMLST

Post issues at https://github.com/lmc297/seq2mlst/issues

### Citation

#### If you found the seq2mlst tool and/or its source code to be useful, please cite:

"Carroll, Laura M. 2017. seq2mlst: *In silico* multi-locus sequence typing. Version 1.0.0. https://github.com/lmc297/seq2mlst."

#### To cite PubMLST (which houses the MLST databases that seq2mlst uses), please cite:

Maiden, Martin CJ, and Keith A. Jolley. 2010. "BIGSdb: Scalable analysis of bacterial genome variation at the population level." 
*BMC Bioinformatics* 11:595.

#### If you're working with genomic data from a member of the *Bacillus cereus* group, you may fine my tool, BTyper, to be useful:

Carroll, Laura M., Jasna Kovac, Rachel A. Miller, Martin Wiedmann. 2017. Rapid, high-throughput identification of 
anthrax-causing and emetic *Bacillus cereus* group genome assemblies using BTyper, a computational tool for virulence-based 
classification of *Bacillus cereus* group isolates using nucleotide sequencing data. 
*Applied and Environmental Microbiology* 2017 Jun 16. pii: AEM.01096-17. doi: 10.1128/AEM.01096-17.

------------------------------------------------------------------------


## Quick Start
  
#### Command structure:
  
```
seq2mlst -t [input data type] -i [input file(s)] -o [output directory] -m ["Genus species"] [options...]
```

For help, type `seq2mlst -h` or `seq2mlst --help`

For your current version, type `seq2mlst --version`

#### Sample commands and analyses:

**Using a fasta/multifasta containing 1 or more closed *Staphylococcus aureus* genomes:**
  
```
seq2mlst -t seq -i my_genomes.fasta -o /path/to/output_directory -m "Staphylococcus aureus"
```

**Using a fasta file containing contigs or scaffolds from a *Salmonella enterica* genome 
(concatenates contigs/scaffolds into a pseudochromosome):**
  
```
seq2mlst -t seq -i my_draftgenome.fasta -o /path/to/output_directory --draft_genome -m "Salmonella enterica"
```

**Using ILLUMINA paired-end reads from a *Campylobacter jejuni* isolate in fastq.gz format (calls SPAdes to assemble):**
  
```
seq2mlst -t pe -i forward_reads.fastq.gz reverse_reads.fastq.gz -o /path/to/output_directory -m "Campylobacter jejuni"
```

**Using ILLUMINA single-end reads from a *Vibrio cholerae* isolate in fastq.gz format (calls SPAdes to assemble):**
  
```
seq2mlst -t se -i illumina_reads.fastq.gz -o /path/to/output_directory -m "Virbrio cholerae"
```

**Using ILLUMINA single- or paired-end reads from a *Klebsiella pneumoniae* isolate in SRA (sequence read archive) 
format (calls SPAdes to assemble):**
  
```
seq2mlst -t sra -i illumina_reads.sra -o /path/to/output_directory -m "Klebsiella pneumoniae"
```

**Using an SRA accession number corresponding to an *Escherichia coli * isolate sequenced using ILLUMINA single- or paired-end
reads (downloads reads from SRA, calls SPAdes to assemble):**
  
```
seq2mlst -t sra-get -i SRR5901521 -o /path/to/output_directory -m "Escherichia coli#2"
```

------------------------------------------------------------------------


 ## Installation
  ### Install seq2mlst using Homebrew (macOS users)
  
  seq2mlst and its dependencies can be installed using <a href="https://brew.sh/">Homebrew</a>.
  
  1. First, install Homebrew, if necessary, by running the following command from your terminal:
  
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Install pip, if necessary, by running the following command from your terminal:

```
sudo easy_install pip
```

3. Install Biopython, if necessary, by running the following command from your terminal:

```
pip install biopython
```
Note: if you don't have permissions, you may need to use sudo:

```
sudo pip install biopython
```

4. Tap Brewsci/science, if necessary, by running the following command from your terminal:
  
```
brew tap brewsci/science
```

5. Tap Brewsci/bio, if necessary, by running the following command from your terminal:

```
brew tap brewsci/bio
```

6. Tap seq2mlst by running the following command from your terminal:
  
```
brew tap lmc297/homebrew-seq2mlst
```

7. Install seq2mlst and its dependencies by running the following command from your terminal:
  
```
brew install seq2mlst
```

### Download and run seq2mlst using source file (macOS and Ubuntu)

1. To run seq2mlst, please download and install the following dependencies, if necessary:
  
  <a href="https://www.python.org/downloads/"> Python v. 2.7</a>
  
  <a href="http://biopython.org/DIST/docs/install/Installation.html"> Biopython v. 1.6.9</a>
  
  <a href="https://github.com/Homebrew/homebrew-science/blob/master/blast.rb">BLAST+ v. 2.4.0 or higher</a>
  
  <a href="https://github.com/Homebrew/homebrew-science/blob/master/spades.rb">SPAdes v. 3.9.0 or higher</a>
  
  <a href="https://github.com/ncbi/sra-tools/wiki/HowTo:-Binary-Installation">SRA toolkit v. 2.8.0 or higher</a>
  
  2. Download the seq2mlst's source file, and store it in your directory of choice:

https://github.com/lmc297/seq2mlst/raw/master/archive/seq2mlst-1.0.0.tar.gz

3. Extract seq2mlst program

```
tar -xzvf seq2mlst-1.0.0.tar.gz
```

Note: to ensure that seq2mlst works correctly, make sure the MLST database directory ("seq_mlst_db") remains in the same 
directory as the seq2mlst executable (stored as "seq2mlst").

4. To run seq2mlst, call Python 2.7 and supply the full path to the seq2mlst executable:

```
python /path/to/executable/seq2mlst [options...]
```

Note: In the examples below, seq2mlst commands are shown as ```seq2mlst [options...]```. If you are calling seq2mlst from 
the source file (i.e. you didn't install seq2mlst using Homebrew), keep in mind that you may have to call python and supply 
the path to seq2mlst to execute the program: ```python seq2mlst [options...]```.


------------------------------------------------------------------------
  
  
  ## Usage and Options
  ### Input File Formats
  
  The command line version of seq2mlst supports the following file formats as input:
  
1. **Nucleotide sequences in fasta or multifasta format** (1 fasta file per genome or multiple genomes per fasta file)

2. **Draft genome contigs and scaffolds in fasta format** (1 fasta file per genome)

3. **Paired-end ILLUMINA reads in gzipped fastq (.fastq.gz) format** (two separate fastq.gz files per genome, one for forward 
reads and one for reverse reads)

4. **Single-end ILLUMINA reads in gzipped fastq (.fastq.gz) format** (one fastq.gz file per genome)

5. **Paired-end or single-end ILLUMINA reads in sra format** (one sra file per genome)

6. **Sequence Read Archive (SRA) accession numbers corresponding to genomes sequenced with paired-end or single-end ILLUMINA
reads** (one SRA accession number per genome)

### Required Arguments

seq2mlst can be run from your terminal with the following command line:
  
```
seq2mlst -t [input data type] -i [input file(s)] -o [output directory] -m "Genus species" [options...]
```

Required arguments are:
  
  
**-t/-\-type [seq, pe, se, sra, sra-get]**
Input data type. Specify the format of the input data using one of the following strings: seq (a file in fasta or multifasta
format), pe (ILLUMINA paired-end reads, forward and reverse, in two separate fastq.gz files), se (ILLUMINA single-end reads in
one fastq.gz file), sra (Single- or paried-end ILLUMINA reads in one SRA file), sra-get (SRA accession number associated with 
a genome sequenced using single- or paried-end ILLUMINA reads)

**-i/-\-input [string]**
Path to input fasta file, fastq.gz file(s), sra file, or SRA accession number. For paired-end ILLUMINA reads in separate 
files, the path to the fastq.gz file containing forward reads should be specified first, followed by the path to the fastq.gz 
file containing reverse reads, with the two paths separated by a single space.

**-o/-\-output [string]**
Path to desired output directory. Specify the path to the output directory where a results directory (seq2mlst_final_results)
containing output files will be created.

**-m/-\-mlst [string]**
Bacterial database to use for MLST, surrounded by quotation marks, e.g. "Salmonella enterica", "Staphylococcus aureus", 
"Listeria monocytogenes", etc.


### Optional Arguments

Options that can be specified in seq2mlst include the following:
  
**-\-draft_genome**
For use with a draft genome (contigs or scaffolds) in fasta format (-\-input my_contigs.fasta -\-type seq). 
If -\-draft_genome is included in the command, seq2mlst creates a pseudochromosome by concatenating contigs or scaffolds 
in a fasta file and inserting a spacer sequence ("NNnnNNnnNNnnNNnn") between them. This option is ommitted by default.

**-\-spades_m [integer]**
Memory limit for SPAdes in Gb. Optional argument for use with ILLUMINA reads (-\-type pe, -\-type se, -\-type sra, or 
-\-type sra-get). seq2mlst passes this parameter to the -m/-\-memory option in SPAdes. Default is set to 250, the default 
for SPAdes.

**-\-spades_t [integer]**
Number of threads for SPAdes. Optional argument for use with ILLUMINA reads (-\-type pe, -\-type se, -\-type sra, or 
-\-type sra-get). seq2mlst passes this parameter to the -t/-\-threads option in SPAdes. Default is set to 16, the default 
for SPAdes.

**-\-spades_k [integer,integer,integer,...]**
Comma-separated list of k-mer sizes to be used for SPAdes (all values must be odd, less than 128 and listed in ascending 
order). Optional argument for use with ILLUMINA reads (-\-type pe, -\-type se, -\-type sra, or -\-type sra-get). seq2mlst 
passes this parameter to the -k option in SPAdes. Default is set to 77.
Note: We recommend selecting optimum k-mer size(s) for your specific data set by consulting the SPAdes documentation. 
Currently, SPAdes recommends using -k 21,33,55,77 for 150 bp ILLUMINA paired-end reads, and -k 21,33,55,77,99,127 for 
250 bp ILLUMINA paired-end reads. 


------------------------------------------------------------------------
  
  
## Output Directories and Files
  
A single seq2mlst run will deposit the following in your specified output directory (-\-output):
  
**seq2mlst_final_results**
*directory*
Final results directory in which seq2mlst deposits all of its output files. seq2mlst creates this directory in your specified
output directory (-\-output) 

***your_genome_final_results.txt***
*file*
Final results text file, 1 per input genome. seq2mlst creates this final results text file, which contains a tab-separated 
line, containing the isolate's sequence type (ST), if available, and the corresponding allelic types (AT). The best-matching 
allele is reported at each locus; an allele that does not match with 100\% identity or coverage is denoted by an asterisk 
(\*), while an allele that is not detected in the genome at the given e-value threshold is denoted by "?". If a sequence type
cannot be determined using the best-matching allelic types, a "?" is listed in its place. A ST that is detemined using any 
best-matching alleles that did not match with 100\% identity or coverage is denoted by \*, regardless of whether all 7 
alleles could be associated with a ST or not.

**genefiles**
*directory*
Directory in which seq2mlst deposits genefiles, (multi)fasta files which contain the sequences of all genes detected in 
a run. seq2mlst creates this directory within the seq2mlst_final_results directory within your specified output directory 
(output_directory/seq2mlst_final_results/genefiles).

***some_gene_genefile.fasta***
*file*
seq2mlst genefiles, (multi)fasta files which contain the sequences of all genes detected in a run. 1 file per each allele 
is created files are created, and if seq2mlst is run using more than 1 genome as input (either in multifasta format, or if 
seq2mlst is run in a loop), genes from each genome are aggregated together in each genefile. These files are formatted so you
can easily input them into your favorite aligner, phylogenetic tree construction program, the NCBI BLAST server, etc.

**isolatefiles**
*directory*
Directory in which seq2mlst deposits results directories for individual genomes. seq2mlst creates this directory within the 
seq2mlst_final_results directory within your specified output directory 
(output_directory/seq2mlst_final_results/isolatefiles).

***your_genome_results***
*directory*
Directory in which seq2mlst deposits additional results files for each input genome. seq2mlst creates this directory within 
the isolatefiles directory (output_directory/seq2mlst_final_results/isolatefiles/*your_genome*_results). Within this 
directory, you'll find detailed tab-separated results files for each typing analysis performed, as well as fasta files 
containing genes extracted from the genome in question. 


------------------------------------------------------------------------


## References

#### Source code (most of it is borrowed from my BTyper program)

Carroll, Laura M., Jasna Kovac, Rachel A. Miller, Martin Wiedmann. 2017. Rapid, high-throughput identification of 
anthrax-causing and emetic *Bacillus cereus* group genome assemblies using BTyper, a computational tool for virulence-based 
classification of *Bacillus cereus* group isolates using nucleotide sequencing data. 
*Applied and Environmental Microbiology* 2017 Jun 16. pii: AEM.01096-17. doi: 10.1128/AEM.01096-17.

#### Dependencies

Bankevich, Anton, et al. SPAdes: A New Genome Assembly Algorithm and Its Applications to Single-Cell Sequencing. *Journal of Computational Biology* 2012 May; 19(5): 455-477.

Camacho, Christiam, et al. BLAST+: architecture and applications. *BMC Bioinformatics* 2009 10:421.

Cock, Peter J., et al. Biopython: freely available Python tools for computational molecular biology and bioinformatics. *Bioinformatics* 2009 June 1; 25(11): 1422-1423.

Leinonen, Rasko, et al. The Sequence Read Archive. *Nucleic Acids Research* 2011 Jan; 39(Database issue): D19–D21.

#### Typing Methods

PubMLST *Bacillus cereus* MLST database (https://pubmlst.org/bcereus/), based on Jolley, Keith A. and Martin CJ Maiden. BIGSdb: Scalable analysis of bacterial genome variation at the population level. *BMC Bioinformatics* 2010 11:595.




