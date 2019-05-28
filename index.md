## Welcome to GitHub Pages
Welcome to my Galaxy project. This exercise is a reproduction of a cancer anaysis using an integrated variant analysis pipeline. What does that mean? First lets talk about  "Integrated Variant".The term is used to describe exome and transcriptome sequencing data derived from tumours specifically looking at variations that fall under three general categories. Gene mutations, differential gene expression and structrural variations. Due to advent of next generation sequencing technologies it has become possible to obtain sequence information from tumours that would provide the researcher a comprehensive genomic profile of the tumour. This mutl-faceted approach holds strong promise in persosnalized oncology

The project consists of three pipelines;

## Exome Analysis Pipeline
The work commences when we input our exome resequence data and map the sequence reads to the Hg19 genome. The task of mappig is accomplished using the **BWA** tool. Next PCR artifacts and duplicates are removed using **Picard**. Once this is completed the **Varscan** utility is used to call variants (Indels & SNP's). Below is the link to the galaxy page which should display all the pipelines data inputs,outputs and data visualization tools.
[https://usegalaxy.org:/u/lakshmanw/h/imported-exome-basics-analysis-mp2](URL)


## Transcriptome Analysis Pipeline
During this step RNA-seq data is used as the primary input. The **TopHat** utility is then used to map the reads and **Varscan**used to identify gene fusions and call other variants.**Cufflinks** is used quantify gene expression and the results fed into the variant analysis pipepline. Galaxy page link showing pipelines, data inputs/outputs, below;
[https://usegalaxy.org:/u/lakshmanw/h/transcriptome-analysis](URL)

## Integrated Variant Analysis Pipeline
This step takes inputs (variants) from the exome and transcription analysis pipes. First mapped RNA-seq data (no fusions) is run on cufflinks to remove artifacts. Next the annovar tool is used to annotate the variants, find expressed rare and deletrious variants. The genes are identified and the information is run against the drug-gene interaction database [www.dgidb.org](url). Finally a summary of the genes, mutations and potential drugs is generated. Below is the link all the pipelines and data;
[https://usegalaxy.org:/u/lakshman/h/-integrated-variant-analysis-new](URL)

## Bugs and Issues:
Running the pipelines presented no issues in general for the exome analysis and the transcriptome analysis workflows. However i run into some problems running the Integrated Variant Analysis Pipe. 
The pipelines consists of 27 steps and everything works as it should till we get to step 20. This step takes inputs from step 19 where the Annovar tool is used to annotate our variants. The next critical step in our analysis requires providing information from our rare and deletrious mutants and inputing this into the Drug-Gene interaction database. The outputs that we would generate from this query would provide information on drug-gene interactions and potential druggability. This is where the critical failure occurs. Upon there investigation the problem seems to lie with a utitlity  called `dgidb_annotator`. In light of this I submitted a ticket to the galaxy development team to hopefully get the bug fixed. The issue seems to lie with the version of the dgidb annotator tool. The tool fails to pick up annotation for valid gene ID's and instead returns an empty green "success" data set.
The dev team worked around the issue and updated the tool version. I still run into the same issue after this.

## Solution:
 Instead of relying on the defective dgidg annotator tool i decided to manually input the information of my rare and deletrious mutants into the dgidb database
 ### About dgidb
 The drug–gene interaction database (DGIdb, www.dgidb.org) consolidates, organizes and presents drug–gene interactions and gene druggability information from papers, databases and web resources. DGIdb normalizes content from 30 disparate sources and allows for user-friendly advanced browsing, searching and filtering for ease of access through an intuitive web user interface, application programming interface (API) and public cloud-based server image.
This is the list of the variants generated from my analysis up to step 19;
`Kras, Notch 1, TP553, TSC2, ZMYM2, ZNF384`







# Next describe the software used for the pipelines
## exome analysis software: BWA, picard Varscan
### Transcriptome analysis software: Tophat, picard cufflinks, Varscan
### Integrated Variant analysis: Varscan, cufflink, annovar


## Next report bugs and issues

## Links to data in galaxy

## Final report

You can use the [editor on GitHub](https://github.com/lmarkal/Galaxy-Integrated-variant-analysis/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)


```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/lmarkal/Galaxy-Integrated-variant-analysis/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
