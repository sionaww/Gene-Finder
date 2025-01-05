# Gene-Finder
GeneFinder: Gene Finder for Pathogen Analysis

## Project Description

This project involves building a gene-finding tool to analyze DNA sequences from a Salmonella pathogen and identify potential protein-coding genes using Open Reading Frames (ORFs). The goal is to develop a simple gene-finding strategy that compares known genomic sequences with randomly shuffled "garbage" sequences to assess the likelihood of a sequence being a gene. This can be used to help researchers study genomic regions that are essential to Salmonella-specific pathogenic processes.The gene-finding strategy focuses on identifying long open reading frames(ORFs) of a DNA seqience, which are typically longer in coding regions compared to noncoding sequences. 

## Technologies Used

Python 3
Jupyter Notebook
Bioinformatics concepts (ORFs, DNA sequencing)
Libraries: random (for generating shuffled DNA sequences)
Prerequisites

## Installation
To run this project, you'll need:

Python 3.x installed on your machine
Jupyter Notebook environment (e.g., Anaconda or JupyterLab)
random library (comes built-in with Python)
Installation Instructions

Clone this repository to your local machine:
git clone https://github.com/yourusername/GeneFinder.git
Navigate to the project directory:
cd GeneFinder
Open the Jupyter Notebook:
jupyter notebook
Open GeneFinder.ipynb in the notebook interface.

## How to Use

### Step 1: Loading DNA Sequences
The project includes a sequence file, X73525.fa, which contains the Salmonella genomic sequence. You can load the sequence into Python using the loadSeq function.

X73525 = loadSeq("X73525.fa")

### Step 2: Finding ORFs
To identify the longest ORFs in a DNA sequence (forward strand), use the longestORFV2 function. You can find ORFs on both the forward and reverse strands using longestORFBothStrands.

longestORF = longestORFBothStrands(X73525)
print(longestORF)
### Step 3: Generating Noncoding Sequences
Generate random, shuffled DNA sequences using the longestORFNoncoding function to assess the expected length of ORFs in noncoding DNA.

longestORFLength = longestORFNoncoding(X73525, 50)
print(longestORFLength)
### Step 4: Identifying Potential Genes
To identify genes in a sequence, run the geneFinder function. The function returns a list of genes found, along with their coordinates and protein sequences.

minLen = 693  # Define a threshold based on the noncoding ORF length
geneList = geneFinder(X73525, minLen)
printGenes(geneList)
### Step 5: BLASTing Protein Sequences
Once you identify potential genes, you can BLAST their protein sequences to find related sequences and predict gene functions. BLAST (Basic Local Alignment Search Tool) is an online tool provided by NCBI to compare nucleotide or protein sequences to known sequences in various databases. Here's how you can use it:

Select a gene from your list and obtain its protein sequence (e.g., using the codingStrandToAA function).
Visit NCBI BLAST: Open NCBI BLAST in your browser.
BLAST the protein sequence:
Go to Basic BLAST and select the Protein Blast option.
Paste the protein sequence into the input box.
Click the "BLAST" button to start the search.
Review the results:
The BLAST search will return a list of sequences similar to your protein, sorted by relevance.
The Descriptions section will show the closest matches, including their names and organisms.
Clicking on a hit will provide more details, such as the function of the gene or protein and where it’s found in various organisms.
Interpret the results: Based on the BLAST results, you can infer the function of your identified gene. For example, if your gene sequence closely matches a gene involved in the immune response, it might suggest that your identified gene is involved in a similar function.
### Step 6: Analyzing New Genomic Data
For a mystery sequence (e.g., salDNA.fa), you can apply the same gene-finding pipeline:

salDNA = loadSeq("salDNA.fa")
geneListSalmonella = geneFinder(salDNA, minLen)
printGenes(geneListSalmonella)
You can then run the identified genes through BLAST to determine their function.

## Project Structure

GeneFinder.ipynb: Jupyter notebook containing the code for the gene-finding algorithm.
X73525.fa: Salmonella genomic sequence file used for analysis.
salDNA.fa: Mystery genomic sequence (for testing and finding new genes).
README.md: Project documentation (this file).

**Key Functions**

loadSeq(filename): Loads a DNA sequence from a .fa file.
oneFrameV2(DNA): Identifies the longest open reading frame (ORF) in a single reading frame.
longestORFBothStrands(DNA): Finds the longest ORF in both the given DNA strand and its reverse complement.
longestORFNoncoding(DNA, numReps): Generates shuffled DNA sequences to determine the maximum ORF length in noncoding sequences.
geneFinder(DNA, minLen): Identifies genes in a DNA sequence based on the ORF length threshold.
printGenes(geneList): Prints the gene results from geneFinder in a readable format.
Example Output

Here is an example of output generated by geneFinder:

## Example of a gene list output
[[34, 55, 'MKKAGFVADKSA'], [120, 160, 'MGDPIQEKNLMD'], [250, 300, 'MKVGAQSDVKGY']]
Gene Finder Results
For each gene found:

Beginning and End Coordinates: Positions of the gene in the original DNA sequence.
Protein Sequence: The translated protein sequence.

## Conclusion

This gene-finding tool helps identify potential protein-coding genes in bacterial genomic sequences, such as those from Salmonella. By comparing real DNA sequences to randomly shuffled sequences, the tool assesses the likelihood that a sequence is genuinely coding for a protein. The BLAST search helps to confirm the function of the genes found, making this tool useful for genomic research and pathogen analysis.
## License 
This project is licensed under the Computing for Biologists textbook
