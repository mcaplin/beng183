# RNA-Seq (RNA Sequencing)
1. [Introduction](#231)
2. [Overivew of 3C methods](#232)<br>
    2.1. [Specificity](#2321)<br>
    2.2. [Through-put and resolution](#2322)
3. [Hi-C](#233)
4. [ChIA-PET](#234)
5. [Selected methods comparison](#235)




## Introduction<a name="231"></a>

RNA-Seq is a tool that uses next-generation sequencing technologies to profile the RNA transcriptome. RNA-Seq is a high throughput tool that can provide much more in depth analysis of transcriptomes compared to other methods.

> In this analysis, we will be going over the general idea of RNA-Seq and some of the popular tools for its use.

##### RNA-Seq General Workflow
- Select Samples of Interest
- Isolate RNAs
- Generate cDNA, fragment and select size, add sequencing adaptors
- Sequence
- Map to genome, transcriptome and predicted exon junctions
- Downstream analysis

![fig1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2949280/bin/nihms229948f1.jpg "Typical RNA-Seq Experiment")
>[figure 1](#1)<br>
>Basic example of an RNA-seq experiment

## Why RNA-Seq?<a name="232"></a>

RNA-Seq offers many advantages over previous methods of transcriptome profiling.

These are the advantages and disadvantages compared to Microarrays [[1]](#1):
<table>
 <tbody>
    <tr>
        <th>RNA-Seq Advantages</td>
		<th>MicroArray advantages</td>
    </tr>
	<tr>
		<td>
			<ul>
		<li>Higher resolution</li>
		<li>Requires less RNA</li>
		<li>Detect genes with low expression</li>
		<li>Detect splice variants</li>
		<li>Lower biases - does not use probes or primers</li>
		<li>Not dependent on existing genome data</li>
	</ul>
	</td>
	<td>
		<ul>
		<li>More cost-efficient</li>
		<li>Less complex analysis</li>
		<li>Requires Less computing power</li>
	</ul>
	</td>
</tr>
 </tbody>
</table>


## Methods of Analysis
RNA-Seq has many different applications depending on the goal of the experiment. There is no optimal pipeline for every scenario, and as such, there are a variety of protocols to quantify RNA.
![fig2](https://media.springernature.com/lw785/springer-static/image/art%3A10.1186%2Fs13059-016-0881-8/MediaObjects/13059_2016_881_Fig1_HTML.gif "RNA-Seq roadmap")
>[figure 2](#2)<br>
>The image above shows the generic steps for RNA-seq analysis. This can be split into three main parts: Pre-analysis, Core-analysis, and Advanced-analysis. We will go over each step and some of the tools used.
### 1) Pre-Analysis
Before we can analyze anything, first we must retrieve raw reads of a sequence.
Two tools to do this are:
- FastQC: *tool to perform analysis on Illumina reads* 
- NGSQC: *tool to perform analysis on any platform* 
After getting the raw reads, we discard low quality reads, trim adaptor sequences, and eliminate poor-quality bases. [2](#2)

> Now that we've got our reads, we can begin mapping them to the genome
### 2) Core-Analysis
There are different types of alignment tools for different purposes. The tools you use depend on whether or not you have a reference genome, the types of reads you have, and the degree of specificity you are looking for in your results.
#### Alignment tools with a reference genome:

##### Short reads:
<table>
 <tbody>
    <tr>
        <th>Method</td>
		<th>Description</td>
    </tr>
	<tr>
		<td>
			SOAP (short oligonucleotide alignment program)
	</td>
	<td>
		Efficiently align large amounts of short reads on to reference sequences using Illumina sequencing. Allows gaps and mismatched reads. [3](#3)
	</td>
	<tr>
		<td>
			STAR (Spliced Transcripts Alignment to a Reference)
		</td>
		<td>
			Unbiased de novo detection of canonical junctions. Can discover non-canonical splices and chimeric transcripts. Can map full-length RNA sequences. [4](#4)
		</td>
	</tr>
	<tr>
		<td>
			Eland
		</td>
		<td>
			Faster than SOAP. Gives more information about repetitive structures and alternative mapping. Meant for short sequences (under 32bp) but can map longer reads with additional scripts. [5](#5)
		</td>
	</tr>
	<tr>
		<td>
			BWA (Burrows-Wheeler Alignment tool)
		</td>
		<td>
			Align short sequences onto a large genome, allowing for mismatches and gaps. [6](#6)
		</td>
	</tr>
</tr>
 </tbody>
</table>


##### Long Reads:
<table>
</tbody>
    <tr>
        <th>Method</td>
		<th>Description</td>
    </tr>
<tr>
	<td>
		TopHat
	</td>
	<td>
		Align reads to the genome and discover transcript splice sites [7](#7)
	</td>
</tr>
</tbody>
</table>

#### Alignment tools with no reference genome:
<table>
</tbody>
    <tr>
        <th>Method</td>
		<th>Description</td>
    </tr>
<tr>
	<td>
		Oases
	</td>
	<td>
		Assemble RNA-seq reads without a reference gehome [8](#8)
	</td>
</tr>

</tbody>
</table>
Oases: 

SOAPdenovo-Trans: higher contiguity, lower redundancy, faster execution
https://arxiv.org/ftp/arxiv/papers/1305/1305.6760.pdf
https://www.ncbi.nlm.nih.gov/pubmed/24532719?dopt=Abstract

### 3) Advanced Analysis


#### 1) Specificity - What does _one, all, many_ mean<a name="2321"></a>
‘1’, ‘Many’ and ‘All’ indicate how many loci are interrogated in a given experiment. For example, ‘1 versus All’ indicates that the experiment probes the interaction profile between 1 locus and all other potential loci in the genome. ‘All versus All’ means that one can detect the interaction profiles of all loci, genome-wide, and their interactions with all other genomic loci [1].

These kind of specificity is determined by the primer when people use **specific primers** before PCR. 

#### 2) Through-put and resolution<a name="2322"></a>
Hi-C techniques has the highest through-put (billion reads per sample) but suffering of a relative low resolution of 0.1-1Mb. However, the other methods usually have a higher resolution  around 1kb. For more details one can refer to table2 in [2].

## 2.3.3 Hi-C<a name="233"></a>
Hi-C is the highest through-put version of 3C-derived technologies. Due to the decreasing cost of 2nd generation sequencing, hi-c is widely used.

The principle of Hi-C can be illustrated as:
![](/assets/hic.gif)


##### Hi-C critical steps [8] 
- Fixation: keep DNA conformed
- Digestion: enzyme frequency and penetratin
- Fill-in: biotin for junction enrichment
- Ligation: freeze interactions in sequence
- Biotin removal: junctions only
- Fragment size: small fragments sequence better
- Adapter ligation: paired-end and indexing
- PCR: create enough material for flow cell

##### Hi-C derived techniques 
- Hi-C original: [Lieberman-Aiden et al., Science 2010](doi: 10.1126/science.1181369)
- Hi-C 1.0: [Belton-JM et al., Methods 2012](doi: 10.1016/j.ymeth.2012.05.001)
- In situ Hi-C: [Rao et al., Cell 2014](doi: 10.1016/j.cell.2014.11.021)
- Single cell Hi-C: [Nagano et al., Genome Biology 2015](https://doi.org/10.1186/s13059-015-0753-7)
- DNase Hi-C [Ma, Wenxiu, Methods et al](https://www.ncbi.nlm.nih.gov/pubmed/25437436)
- Hi-C 2.0: [Belaghzal et al., Methods 2017](https://www.ncbi.nlm.nih.gov/pubmed/28435001)
- DLO-Hi-C: [Lin et al., Nature Genetics 2018](https://doi.org/10.1038/s41588-018-0111-2)
- Hi-C improving: [Golloshi et al., Methods 2018](https://www.biorxiv.org/content/biorxiv/early/2018/02/13/264515.full.pdf)
- Arima 1-day Hi-C: [Ghurye et al., BioRxiv 2018](https://www.biorxiv.org/content/early/2018/02/07/261149)

## 2.3.4 ChIA-PET<a name="234"></a> 
ChIA-PET is another method that combines ChIP and pair-end sequencing to analysis the chromtin interaction. It allows for targeted binding factors such as: estrogen receptor alpha, CTCF-mediated loops, RNA polymerase II, and a combination of key architectural factors. on the one hand, it has the benefit of achieving a higher resolution compared to Hi-C, as only ligation products involving the immunoprecipitated molecule are sequenced, on the other hand, ChIA-PET has systematic biases due to ChIP process:
- Only one type of binding factor selected
- Different antibodies
- ChIP conditions


## 2.3.5 Selected methods comparison<a name="235"></a> 
<table>
 <tbody>
    <tr>
        <th>Method</td>
        <th>Targets</td>
        <th>Resolution</td>
        <th>Notes</td>
    </tr>
    <tr>
        <td>3C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0535">[3]</a></td>
        <td>one-vs-one</td>
        <td>~1–10 kb<br></td>
        <td><ul><li>Sequence of bait locus must be known</li><li>Easy data analysis</li><li>Low throughput</li></ul></td>
    </tr>
    <tr>
    <td>4C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0545">[4]</a></td>
    <td>one-vs-all</td>
    <td>~2 kb</td>
    <td><ul><li>Sequence of bait locus must be known</li><li>Detects novel contacts</li><li>Long-range contacts</li></ul></td>
    </tr>
    <tr>
    <td>5C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0550">[5]</a></td>
    <td>many-vs-many</td>
    <td>~1 kb</td>
    <td><ul><li>High dynamic range</li><li>Complete contact map of a locus</li><li>3C with ligation-mediated amplification (LMA) of a ‘carbon copy’ library of oligos designed across restriction fragment junctions of interest
3C</li></ul></td>
    </tr>
    <tr>
    <td>Hi-C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0300">[6]</a></td>
    <td>all-vs-all</td>
    <td>0.1–1 Mb</td>
    <td><ul><li>Genome-wide nucleosome core positioning</li><li>Relative low resolution</li><li>High cost</li></ul></td>
    </tr>
    <tr>
    <td>ChIA-PET <a href="http://refhub.elsevier.com/S0168-9525(15)00063-3/sbref1405">[7]</a></td>
    <td>Interaction of whole genome mediated by protein</td>
    <td>Depends on read depth and the size of the genome region bound by the protein of interest</td>
    <td><ul><li>Lower noise with ChIP</li><li>Biased method since selected protein</li></ul></td>
    </tr>
 </tbody>
</table>

















# Reference

<a name="1"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2949280/">[1]</a> Wang, Zhong et al. “RNA-Seq: a revolutionary tool for transcriptomics” Nature reviews. Genetics vol. 10,1 (2009): 57-63. <br>

<a name="2"></a><a href="https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0881-8">[2]</a> Conesa, Ana, et al. “A Survey of Best Practices for RNA-Seq Data Analysis.” Genome Biology, BioMed Central, 26 Jan. 2016 <br>

<a name="3"></a><a href="https://www.ncbi.nlm.nih.gov/pubmed/18227114">[3]</a> Ruiqiang Li, Yingrui Li, Karsten Kristiansen, Jun Wang; SOAP: short oligonucleotide alignment program, Bioinformatics, Volume 24, Issue 5, 1 March 2008, Pages 713–714 <br>

<a name="4"></a><a href="https://academic.oup.com/bioinformatics/article/29/1/15/272537">[4]</a> Alexander Dobin, Carrie A. Davis, Felix Schlesinger, Jorg Drenkow, Chris Zaleski, Sonali Jha, Philippe Batut, Mark Chaisson, Thomas R. Gingeras; STAR: ultrafast universal RNA-seq aligner, Bioinformatics, Volume 29, Issue 1, 1 January 2013, Pages 15–21 <br>

<a name="5"></a><a href="massgenomics.org/2008/05/short-read-aligners-maq-eland-and-others.html">[5]</a> dkoboldt. “Short Read Aligners: Maq, Eland, and Others.” MassGenomics, 14 May 2008 <br>

<a name="6"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2705234/">[6]</a> Li, Heng and Richard Durbin. “Fast and accurate short read alignment with Burrows-Wheeler transform” Bioinformatics (Oxford, England) vol. 25,14 (2009): 1754-60. <br>

<a name="7"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3334321/">[7]</a> Trapnell, Cole et al. “Differential gene and transcript expression analysis of RNA-seq experiments with TopHat and Cufflinks” Nature protocols vol. 7,3 562-78. 1 Mar. 2012, doi:10.1038/nprot.2012.016 <br>

<a name="8"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3324515/">[8]</a> Schulz, Marcel H et al. “Oases: robust de novo RNA-seq assembly across the dynamic range of expression levels” Bioinformatics (Oxford, England) vol. 28,8 (2012): 1086-92. <br>
