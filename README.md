# BenchmarkResults

The scripts to produce these results are in the repository Benchmark (https://github.com/SarahStrobel/Benchmark).

== Bacillus subtilis

The following files have the predicted terminators for Bacillus subtilis is various forms.

File 1
The set of termination positions based on TermSeq data, but not including predictions that overlap with known terminators or overlap genes.  These are the actual nucleotide positions between which termination is supposed to occur.  NOTE: the strand information is not indicated, but the classification.py script could be augmented to include this.
- in [BED format](https://en.wikipedia.org/wiki/BED_%28file_format%29): Results/Classification/wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes.bed

File 2
The set of terminators.  These are the same positions as within File 1 (wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes.bed) but add 17 nucleotides downstream (to be sure to fully get the poly-U) and 82 nt upstream (to hopefully include the hairpin) so that there are 100 nucleotides in total.  The strand is indicated by '+' or '-' in the last character of each line.
- in BED format: Results/Classification/wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes_long.bed

In generating the files below, File 2 (with the 100-nt sequences) is further filtered by the following criteria:
- Terminators that are more than 150 nucleotides downstream of genes are removed as maybe being suspect (see call to 'position.py' script witin Termi.sh)
- (only relevant to Bacilus subtilis, since the others don't have known terminators) Terminators that are too similar to known terminators are removed.  "too similar" means a BLAST blastn score of >=30 bits
- terminators whose start coordinate is less than 1000000 (for Bacillus subtilis) or 500000 (for other species) are removed because terminators in these genome coordinates were used during parameterization of this benchmark, and might therefore be biased.

File 3
This leads to the set of terminators that can be used as positives.
- in FASTA format: Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.fasta
- in BED format: Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.bed

File 4
The set of terminators (Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.fasta) embedded in genome sequences.
- embedded within native genomic sequences (500 nucs on each side): Results/Embedded/1NegativePerPositive/BS_embedded_predictedTerminators_native.fasta
- embedded within shuffled genomic sequences: Results/Embedded/1NegativePerPositive/BS_embedded_predictedTerminators_native.fasta
- completely shuffled sequences to use as negatives: Results/Embedded/1NegativePerPositive/BS_embedded_shuffledNegatives_shuffled.fasta
