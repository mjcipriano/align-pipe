# align-pipe
=head1 SYNOPSIS

        This script uses BLAST results to locate comparative sequences for an open reading frame,
        then uses MUSCLE on the top hits to create an alignment.  This alignment
        is iteratively run through Mr.Bayes and a masking process to develop
        an optimized phylogenetic tree for comparative evolution.

=head1 DESCRIPTION

        The logical steps for alignpipe are as follows:
        1) Read in commandline arguments (see OPTIONS below)
        2) Get BLAST results
                a) read from the database containing blast_results
                b) or blastp orf_fasta against blastdb
                c) or read from an alignment file
        3) Get an alignment
                a) Run Muscle on the set of blast sequences
        4) Create an initial mask of the alignment data
        5) Iterate tree generation
                a) Run Mr.Bayes on the alignment data
                b) Determine the confidence level of the consensus tree
                c) Compare confidence with acceptable confidence
                d) Update the masking parameters
                e) repeat...
        6) Store the results to the database or an output file
