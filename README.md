# BenchmarkResults

The scripts to produce these results are in the repository Benchmark.

The following files have the predicted terminators for Bacillus subtilis

BS_FILE_Aa:
The set of termination positions based on TermSeq data, but not including predictions that overlap with known terminators or overlap genes.  These are the actual nucleotide positions between which termination is supposed to occur.  NOTE: the strand information is not indicated
in BED format: Results/Classification/wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes.bed

The set of terminators.  These are the positions within wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes.bed but add 17 nucleotides downstream (to be sure to fully get the poly-U) and 82 nt upstream so that there are 100 nucleotides in total.  The strand is indicated by '+' or '-' in the last character of each lines.
in BED format: Results/Classification/wholeGenome_filtered_trim_scaled_BS_predictedNegatives_NO_knownTerminators_NO_genes_long.bed

This list (with the 100-nt sequences) is further filtered by the following criteria:
- terminators that are more than 150 nucleotides downstream of genes are removed as maybe being suspect (see call to 'position.py' script witin Termi.sh)
- (only relevant to Bacilus subtilis, since the others don't have known terminators) terminators that are too similar to known terminators are removed.  "too similar" means a BLAST blastn score of >=30 bits
- terminators whose start coordinate is less than 1000000 (for Bacillus subtilis) or 500000 (for other species) are removed because they were used during parameterization of this benchmark.

The set of terminators that can be used as positives.  They are not redundant with each other or with previously predicted terminators (with BLAST score threshold of 30 bits) and 
in FASTA format: Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.fasta
in BED format: Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.bed

The set of terminators (Results/BLAST/withoutPolluted/cut_BS_predTerm_BLAST_predictedTerminators_NO_knownTerminators_NO_genes_long.fasta) embedded in genome sequences.
embedded within native genomic sequences (500 nucs on each side): Results/Embedded/1NegativePerPositive/BS_embedded_predictedTerminators_native.fasta
embedded within shuffled genomic sequences: Results/Embedded/1NegativePerPositive/BS_embedded_predictedTerminators_native.fasta
completely shuffled sequences to use as negatives: Results/Embedded/1NegativePerPositive/BS_embedded_shuffledNegatives_shuffled.fasta

