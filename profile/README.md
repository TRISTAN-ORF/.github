<div align="center">
<h1>TRISTAN</h1>
  
*Driving coding sequence discovery since 2023*

</div>

## 👋 Introduction

TRISTAN (TRanslational Identification Suite using Transformer Networks for ANalysis) is a set of tools that offer complementary insights towards detecting ORFs that are translated in organisms. 

  
<div align="center">
<img src="https://github.com/TRISTAN-ORF/.github/raw/main/TRISTAN_overview.png" width="800">
</div>

## 🤨 Why TRISTAN?

TRISTAN tools are built using the newest advances in machine learning, aim to adhere closely to best practices in machine learning, step away from manually curated rules for data processing (Let the optimization algorithm handle it!), and are designed with flexibility and modularity in mind.

To illustrate (to expand)
 - No custom positive/negative set
 - Inclusion of full transcriptome
 - separation of training / validation / test set by chromosomes
 - No hardcoded rules altering data/predictions (e.g. multicistronic transcripts, start codon use, ...)
 - PR/ROC AUC scores used for evaluation and benchmarking
 - various output file formats that can be easily plugged into downstream analyses tools
 - output file format customizability
   
## ⁉️ FAQ

**Why not create a model that is trained on both transcript sequence and ribosome profiling data?**

Models trained on sequencing data are susceptible to incorporating biases existent in todays annotations (e.g. codon usage, start codons frequency, ...). On the other hand, models applying ribosome profiling data are restricted by the read depth of the sample and translation profile of the organism.
Both models, in essence, trt to answer different questions (i.e., What ORFs look viable to be translated based on sequence context / What ORFs are actively being translated based on ribosome protected fragment distributions). 
We determined that the combination of both modalities of data within a single model obfuscates the function of that model.

These differences of data also become a problem when evaluating the optimization process. For TIS transformer, all transcripts are viable information, as the sequence of all transcripts is known.
For RiboTIE, only transcripts with mapped reads have valuable information. 
In practice, we do not alter the labels of the positive set for these transcripts (which would require us to solve the question of how many reads are too few to alter target labels to a negative value?) , as the presence of a positive label for an input vector containing zeros (no reads) does not bias the model negatively (there is nothing to learn). 
However, combining both sequence and ribo-seq data would result in the model relying on sequence information more than it does on ribosome profiling data.

In conclusion, the combination of both data modalities raises plenty of hard-to-answer questions and obfuscates the actual function that the optimized model performs, without offering any obvious benefits.
Both tools can be used in combination to offer insights into ORFs of interest, but should be evaluated using a good understanding of the advantages and sensitivies of both approaches. 
