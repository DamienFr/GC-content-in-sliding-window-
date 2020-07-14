# Description

    This script will first calculate, for each nucleotide position, the %GC of the surrounding nucleotid
    sequence according to the window size. 
    For the first nucleotid, half of the window size will be taken from the end of the sequence, because
    this script has been developped for cicular genoms.
    Then, a mean GC% value is computed for each interval of "step" nucleotides.
	
# Window/step rationale

Now, to get the GC% of a every 50nt interval of a genome, you can just calculate the % of G and C nucleotide of these 50 studied nucleotides. If you do that, the signal along the genome will be very noisy, leading to fast variations when you draw the curve.
To soften these fast variations, you can instead calculate for each 50nt intervals, the GC% of the 1000nt surrounding that area. As an example, the 1001-1050nt interval would display the % calculated for nucleotides comprised between positions 526 and 1525.

This is important NOT to just calculate AND display with the same interval because if you do this with a window=step=1000nt for example, you will get few values that differ from each other, drawing a very not nice stairs ...

With window and step different you get a smooth line slowly increasing and slowly decreasing.

# Usage

    perl gc_content.pl --fasta genome.fasta [--window 1000] [--step 100] [--log] [--help] 
    
    
    Arguments details :
    --fasta	Fasta file, (REQUIRED) Can contain multiple sequences: script will produce as many output files as input sequences. Each sequence can be multiline.
    --window 	Window size, (optional, default 1000) Even number ONLY. Sets the number of nucleotides used to calculate the %GC value of each position.
    --step	Step size, (optional, default 100) The output will contain a GC% value every "step" nucleotides. The numbers of values you get is therefore (length genome)/(step).
    --log	(optional) For debugging purposes only
    --help	(optional) Shows this help
   
# Output files

    [input_name].gc_content
    
    column 1: "chr1" for convenience when the program is used to create an input for Circos (www.circos.ca/) 
    column 2: start position of interval
    column 3: end position of interval 
    column 4: GC% of the interval 
    
    example:
    chr1 1 100 0.499
    chr1 101 200 0.5
    chr1 201 300 0.5
    chr1 301 400 0.5
    chr1 401 500 0.5
    chr1 501 600 0.5
    chr1 601 700 0.499
    chr1 701 800 0.5

    [input_name].gc_deviation

    column 1: "chr1" for convenience when the program is used to create an input for Circos (www.circos.ca/) 
    column 2: start position of interval
    column 3: end position of interval 
    column 4: GC deviation of the interval 
    
    example:
    chr1 1 100 0.162
    chr1 101 200 0.16
    chr1 201 300 0.16
    chr1 301 400 0.16
    chr1 401 500 0.16
    chr1 501 600 0.16
    chr1 601 700 0.162
    
# AUTHOR

	Damien Richard, 2019
