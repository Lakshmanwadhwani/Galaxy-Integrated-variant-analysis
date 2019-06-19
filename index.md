## Welcome to GitHub Pages
Welcome to my Galaxy project. This exercise is a reproduction of a cancer anaysis using an integrated variant analysis pipeline. What does that mean? First lets talk about  "Integrated Variant".The term is used to describe exome and transcriptome sequencing data derived from tumours specifically looking at variations that fall under three general categories. Gene mutations, differential gene expression and structrural variations. Due to advent of next generation sequencing technologies it has become possible to obtain sequence information from tumours that would provide the researcher a comprehensive genomic profile of the tumour. This mutl-faceted approach holds strong promise in persosnalized oncology.

## About our tumour sample
For my experiment the source of my exome and transcriptome sequence information was derived from the MIA PaCa-2 cancer cell line. The original cell lines were derived from the Carcinoma of a 65 year old male. The MIA PaCa-2 cell line has been used for decades as a model to study the mechanisms of carcinogenesis in pancreatic cancer. I will be analyzing the targeted exome and whole transcriptome sequence data from the MIA PaCa-2 tumour, in particular the exonic regions of 577 genes that are commonly included in cancer gene cell panels.


The project consists of three pipelines;

## Exome Analysis Pipeline
The work commences when we input our exome resequence data and map the sequence reads to the Hg19 genome. The task of mappig is accomplished using the **BWA** tool. Next PCR artifacts and duplicates are removed using **Picard**. Once this is completed the **Varscan** utility is used to call variants (Indels & SNP's). Below is the link to the galaxy page which should display all the pipelines data inputs,outputs and data visualization tools.Copy and paste the link in your browser to access.
[https://usegalaxy.org/u/lakshmanw/h/imported-exome-basics-analysis-mp2](URL).


## Transcriptome Analysis Pipeline
During this step RNA-seq data is used as the primary input. The **TopHat2** utility is then used to map the reads followed by using **Tophat-fusion** to identify fusions. **Varscan** is then used to identify gene fusions and call other variants.**Cufflinks** is used quantify gene expression and the results fed into the variant analysis pipepline. Galaxy page link showing pipelines, data inputs/outputs, below;
[https://usegalaxy.org/u/lakshmanw/h/transcriptome-analysis](URL). Copy and paste the link into your browser for access.

## Integrated Variant Analysis Pipeline
This step takes inputs (variants) from the exome and transcription analysis pipes. First mapped RNA-seq data (no fusions) is run on **cufflinks** to remove artifacts. Next the **annovar** tool is used to annotate and find expressed rare and deletrious variants. The genes are identified and the information is run against the drug-gene interaction database [www.dgidb.org](url). Finally a summary of the genes, mutations and potential drugs is generated. Below is the link all the pipelines and data. Copy and paste the link in your browser for access.
[https://usegalaxy.org/u/lakshmanw/h/-integrated-variant-analysis-new](URL)

## Bugs and Issues:
Running the pipelines presented no issues in general for the exome and the transcriptome analysis. However i run into some problems running the Integrated Variant Analysis Pipe. 
The pipeline consists of 27 steps and everything works as it should till we get to step 20. This step takes inputs from step 19 where the Annovar tool is used to annotate our variants. The next critical step in our analysis requires providing information from our rare and deletrious mutants and inputing this into the Drug-Gene interaction database. The outputs that we would generate from this query would provide information on drug-gene interactions and potential druggability. This is where the critical failure occurs. Upon there investigation the problem seems to lie with a utitlity  called `dgidb_annotator`. In light of this I submitted a ticket to the galaxy development team to hopefully get the bug fixed. The issue seems to lie with the version of the dgidb annotator tool. The tool fails to pick up annotation for valid gene ID's and instead returns an empty green "success" data set.
The dev team tried to work around the problem by updating the tool version. I still run into the same issue after this.

## Solution:
 Instead of relying on the defective dgidg annotator tool i decided to manually input the information of my rare and deletrious mutants into the dgidb database.

### About dgidb
 The drug–gene interaction database (DGIdb, www.dgidb.org) consolidates, organizes and presents drug–gene interactions and gene druggability information from papers, databases and web resources. DGIdb normalizes content from 30 disparate sources and allows for user-friendly advanced browsing, searching and filtering for ease of access through an intuitive web user interface, application programming interface (API) and public cloud-based server image.
This is the list of the variants generated from my analysis up to step 19;
Kras, Notch 1, TP553, TSC2, ZMYM2,  and ZNF384.


**Final Reports**
We have two general datasets of importance generated by our workflows. The first dataset consists of our list of annonated variants.This contains both deletirous mutations and all other variants. The second dataset consists of our list of deletrious variants annotated with drug gene information and potential drugability from the drug-gene database. 

**Annotated variant tables**

Step 18 of the integrated analysis pipeline produces a data set that includes annotations for each variant. The data is represented by a table consisting of 17 columns. The first five columns define the variant. The annotation describes where the variant occurs in the gene (Chromosome location, start end, exonic,intronic etc..) and the functional impact of the variant. The functional impact is defined by whether the SNP is a synonymous or non-synonymous mutation. Additional annotations include the dbSNP number if available (this indicates if the SNP can be located in the COSMIC cancer database) and other conservation scores from other databses (eg 1000 genomes project, exome sequencing project).
Step 19 produces a dataset that has filtered the large set of variants from step 18 down to just the deletrious mutations. These are the variants that are thought to have a deletrious impact on the function of the gene.The identified deletrious mutations are **Kras, Notch 1, TP553, TSC2, ZMYM2,  and ZNF384**

**Drug-gene interactions and potential druggability**
Contained in my github folders are the results of the annotations of our deletrious variants against the drug-gene interaction database.We have two sets of data tables. The information is represented in a TSV file format and an excel file format. 

The first data table titled **drug-gene interaction** contains the following relevant information; Gene name, name of the potentially effective drug, the source of information, and the associated pubmed ID's.

The second data table titled **Potential druggability** contains the follwoing columns; Gene name, category, and the source organization for the information. Under category column there are three listings; Clinically actionable target, Druggable genome, and the functional pathway of the gene. 
 

**Important Disclaimer from the Drug-Gene Interaction Database:**
Disclaimer: This resource is intended for purely research purposes. It should not be used for emergencies or medical or professional advice
A finding of a drug-gene interaction or potentially druggable category does not necessarily indicate effectiveness (or lack thereof) of any drug or treatment regimen. A finding of no interaction or no potentially druggable category does not necessarily indicate lack of effectiveness of any drug or treatment regimen. Drug-gene interactions or potentially druggable categories are not presented in ranked order of potential or predicted efficacy.

The dgidb.org website does not provide any medical or healthcare products, services or advice, and is not for medical emergencies or urgent situations. IF YOU THINK YOU MAY HAVE A MEDICAL EMERGENCY, CALL YOUR DOCTOR OR 911 IMMEDIATELY. Information contained on this website is not a substitute for a doctor's medical judgment or advice. We recommend that you discuss your specific, individual health concerns with your doctor or health care professional.

I will continue to update the content of this page with more background information on our deleterious variants and implications for therapy.


