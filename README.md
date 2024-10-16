# Loci
Python package representing genomic loci and allowing operations on them [science, genomics]. Fork of GenomicRanges

# Motivation
I have come to Python genomics from working with R, enjoying the whole Bioconductor ecosystem. I quickly searched for a Python package which replaces GenomicRanges, but found only `PyRanges` and a new repo `GenomicRanges`.
In Python there not even have been an implementation of the critical overlap-computation data structure NCList until TODO.

`PyRanges` has very little functions implemented, but is based on Pandas, so familiar to Python programmers. There is also `pyBedTools` which is not really a Python solution but a set of wrappers of syscalls to `bedtools`, and it has on-disk operation mode (slow).

I turned to `GenomicRanges` and started using them, but very quickly ran into various bugs, which I had to fix in the package to compute very basic things. After 3 days of struggle I finally realised that there was a bug in joining two objects (which was called by almost all interval algebra functions). So all the results I computed so far were wrong. At this point I stopped bug-reporting and decided to clone the repo and work on my own.

# Desiderata
What I want to achieve with this package is to
- Port to Pandas: remove mcols, BiocFrames. All additional columns will be Pandas DataFrames.
- Implement import and export functions to read/write data in various formats without using other packages. Imports from warious formats should be done with single function: the constructor.
- Reduce screen space for viewing Loci and for coding: abbreviations for columns and for function names, e.g. use 3-character names: chr, beg, end, str for chromosome, beginning, end and strand.
- Deal properly with chromosome lenghts: every Loci object must have a genome assigned. This should be as simple as adding "hg38" as an argument to the constructor.
- Only one genome per object. There is no point of having separate genomes for each locus.
- Pretty-printing space-savvy in Jupyter and in command line
- Metadata columns can be accessed directly with `[]`
- No internal string operations: no spurious parsing or deparsing anything
- Efficient coverage computation
- Remove GenomicRangesList in favour of simple Python lists
- Drop names of loci. There can be a name column of course.
- Allow for 0-length loci representing particular phosphodiester bonds (-p-) between nucleotides. For instance to represent CRISPR cut sites, recombination points, TSSs etc.

# Name
Loci is a plural nominative of Latin noun locus meaning place. This word is commonly used by genomicists (and all biologists) to refer to contiguous pieces of DNA. Pronunciation is according to Classical Latin /ˈlo.kiː/, not the English pronunciation /ˈloʊsaɪ/, nor German /lotsi/.

