# Modified-SilkSlider
Inference of silk-like structural proteins (SLSPs). This script and the associated python find_glycine-rich_seqs.py are a simplified knock-off of the SilkSlider pipeline published in McDougall et al. 2016. PLoS ONE 11(7): e015928.
See: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0159128 and https://github.com/wwood/SilkSlider

## Dependancies 
DeepTMHMM: https://dtu.biolib.com/DeepTMHMM
SignalP V.5.0: https://services.healthtech.dtu.dk/services/SignalP-5.0/

## Approach
First, glycine-rich sequences were identified using the same approach as McDougall et al. 2016. As SLSPs are trafficked outside of the cell membrane, the exclusion of sequences without a signal peptide ensures the exclusion of any extracellular debris (McDougall et al. 2016). Signal-P v. 5 (Almagro Armenteros et al. 2019) was then used to exclude any sequences lacking a signal peptide followed by DeepTMHMM (Hallgren et al. 2022) to exclude sequences with a transmembrane domain
Gylcine-rich sequences are identified using the same approach as McDougall et al. 2016. Downstream analyses were modified to use an updated Signal P and DeepTMHMM instead of TMHMM. The process is the following:
1) Remove ORFs lacking an N-terminal methionine 
2) Removed sequences that did not have a signal peptide using SignalP
4) Removed the signal peptide from remaining sequences using SignalP
5) Removed sequences that were predicted to have a transmembrane domain by DeepTMHMM
6) Used a sliding window algorithm to identify sequences containing at least 25% glycine within an 80 amino acid window. 

## Usage 
Wrapper script name: find_silk-like_proteins.sh

INPUT: file named <something>.aa (no periods allowed other than the one before .aa)

In the same directory running find_silk-like_proteins.sh you also need to have the accessory scripts find_glycine-rich_seqs.py and select_contigs.pl

FINAL OUT: file named input.aa.glycine-rich.signalp5.deeptmhmm containing glycine-rich sequences with signal peptide and without one or more transmembrane domains
