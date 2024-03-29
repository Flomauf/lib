Most of the scripts use Biopython for the analysis. It must be installed in your environment for using these scripts:

```
pip instal biopython
```

## FastSplit

FastSplit splits a fasta/fastq file into multiple smaller files based on a maximum
number of sequence per file or a maximum cumulated sequences length per file. It can 
also split sequences into multiple sequence at a given length.
This can be useful for online analyses with file size limits (e.g. NCBI Blast). 

```
FastSplit.py [parameters] [value] [file]
```
 
  -file: a fasta/fastq file  
  -parameter:  
    -*length_max* -> maximum cumulated length of sequences per file  
    -*contigs_max* -> maximum number of sequences per file  
    -*length_split* -> split sequences at specific length (output = fasta)  
  -value  

## FastFilt

FastFilt filters out sequences from fasta/fastq files based on a filtering parameter.

```
FastFilt.py [parameter] [value] [file]
```

  -file: a fasta/fastq file  
  -parameter:  
    -*length_max* -> maximum length of contigs  
    -*length_min* -> minimum length of contigs  
    -*seq_present* -> contigs containing the sequence (or base)  
    -*seq_absent* -> contigs not containing the sequence (or base)  
  -value: sequences length (for *length_max* and *length_min*) or a sequence STRING 
  (for *seq_present* and *seq_absent*)  


## FastStats

FastStats can output statistics of a fasta/fastq file (number of sequences, 
maximum/minimum sequences length, total length and sequences length mean/median.

```
FastStats.py [file]
```

  -file: a fasta/fastq file  

## FastCheck

FastCheck scans sequences string and returns nucleotides composition or print sequences 
with only A/T/C/G bases.

```
FastCheck.py [parameter] [file]
```
  -file: a fasta/fastq file  
  -parameters:  
    -*bases_stat* -> sequence nucleotides composition 
    -*filter_non_atgc* -> prints sequences composed of A/T/G/C only.  

## collapse_and_count

Remove duplicate sequences in a fasta file based on sequence description. The count of each
sequence is kept and added in the header.

```
collapse_and_count.py input output
```
  -input: input fasta file (nucl or prot)  
  -output: output fasta file  

## get_maps

Takes a list of Kegg KOs as input in a file and return a list of Kegg pathways with the number of KO including in each pathway.

```
get_maps.py -i FILE [-o FOLDER] [-l FOLDER]
```
  -i: file with KOs  
  -o: output folder [.\]  
  -l: log folder [.\]  

## build_pathways_matrix

The script takes as input pathway counts file generated with get_maps.py and create a count matrix.

```
build_pathways_matrix.py -f FOLDER [-o FILE]
```
  -f FOLDER   folder containing pathways count files  
  -o FILE     output matrix name [KO_matrix.csv]  

## rf_functions

Utility functions for random forests using the randomForest package in R.

```
rf_overfitting_test <- function(table, target, mtry, ntree, index_split, iteration, type, maxnode = NULL, print=TRUE)
```
Compute the difference in Mean Squared Error between the model and predictions. Usefull for determining if a model is overfitting or not.

```
best_rf <- function(table, target, mintree, maxtree, step)
```
Find the best combination of mtry and ntree values in order to obtain the best model.

```
remove_least_imp <- function(table, model, proportion)
```
Only keep most important predictors. Usefull for decomplexing model, lowering overfitting and calculation time.

## gbk_commands

Different functions to use with similar Genbank files. Useful for sequence vizualisation with tools like Clinker.

```
gbk_commands.py find -i [FOLDER]
```
Find genes common to all Genbank files. Duplicated genes are ignored.

  -i: Folder with all Genbank files

```
gbk_commands.py order [-h] -i FOLDER -o FOLDER -t STR
```
Re-order Genbank files considering a gene in common as origin.

  -i: Folder with all Genbank files
  -o: Output folder for all reordered Genbank files
  -t: Target gene considered as origin

```
gbk_commands.py extract [-h] -i FOLDER -o FOLDER -t STR -r NUM
```
Extract region surrounding a specified gene.

  -i: Folder with all Genbank files
  -o: Output folder for all extracted regions
  -t: Target gene
  -r: Sequence length to extract before and after the target

