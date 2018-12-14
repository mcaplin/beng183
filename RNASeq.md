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
After getting the raw reads, we discard low quality reads, trim adaptor sequences, and eliminate poor-quality bases. [[2]](#2)

> Now that we've got our reads, we can begin mapping them to the genome
### 2) Core-Analysis
There are different types of alignment tools for different purposes. The tools you use depend on whether or not you have a reference genome, the types of reads you have, and the degree of specificity you are looking for in your results.
#### Alignment tools with a reference genome:

**Short Reads**
<table>
 <tbody>
    <tr>
        <th>Method</td>
		<th>Description</td>
    </tr>
	<tr>
		<td>
			SOAP (short oligonucleotide alignment program) [[3]](#3) [[3]](#1)
	</td>
	<td>
		Efficiently align large amounts of short reads on to reference sequences using Illumina sequencing. Allows gaps and mismatched reads.
	</td>
	<tr>
		<td>
			STAR (Spliced Transcripts Alignment to a Reference)
		</td>
		<td>
			Unbiased de novo detection of canonical junctions. Can discover non-canonical splices and chimeric transcripts. Can map full-length RNA sequences.
		</td>
	</tr>
	<tr>
		<td>
			Eland
		</td>
		<td>
			Faster than SOAP. Gives more information about repetitive structures and alternative mapping. Meant for short sequences (under 32bp) but can map longer reads with additional scripts.
		</td>
	</tr>
	<tr>
		<td>
			BWA (Burrows-Wheeler Alignment tool)
		</td>
		<td>
			Align short sequences onto a large genome, allowing for mismatches and gaps.
		</td>
	</tr>
</tr>
 </tbody>
</table>
SOAP [[3]](#1)

**Long Reads**
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





















# Reference

<a name="1"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2949280/">[1]</a> Wang, Zhong et al. “RNA-Seq: a revolutionary tool for transcriptomics” Nature reviews. Genetics vol. 10,1 (2009): 57-63. <br>

<a name="2"></a><a href="https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0881-8">[2]</a> Conesa, Ana, et al. “A Survey of Best Practices for RNA-Seq Data Analysis.” Genome Biology, BioMed Central, 26 Jan. 2016 <br>

<a name="3"></a><a href="https://www.ncbi.nlm.nih.gov/pubmed/18227114">[3]</a> Ruiqiang Li, Yingrui Li, Karsten Kristiansen, Jun Wang; SOAP: short oligonucleotide alignment program, Bioinformatics, Volume 24, Issue 5, 1 March 2008, Pages 713–714 <br>

<a name="4"></a><a href="https://academic.oup.com/bioinformatics/article/29/1/15/272537">[4]</a> Alexander Dobin, Carrie A. Davis, Felix Schlesinger, Jorg Drenkow, Chris Zaleski, Sonali Jha, Philippe Batut, Mark Chaisson, Thomas R. Gingeras; STAR: ultrafast universal RNA-seq aligner, Bioinformatics, Volume 29, Issue 1, 1 January 2013, Pages 15–21 <br>

<a name="5"></a><a href="massgenomics.org/2008/05/short-read-aligners-maq-eland-and-others.html">[5]</a> dkoboldt. “Short Read Aligners: Maq, Eland, and Others.” MassGenomics, 14 May 2008 <br>

<a name="6"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2705234/">[6]</a> Li, Heng and Richard Durbin. “Fast and accurate short read alignment with Burrows-Wheeler transform” Bioinformatics (Oxford, England) vol. 25,14 (2009): 1754-60. <br>

<a name="7"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3334321/">[7]</a> Trapnell, Cole et al. “Differential gene and transcript expression analysis of RNA-seq experiments with TopHat and Cufflinks” Nature protocols vol. 7,3 562-78. 1 Mar. 2012, doi:10.1038/nprot.2012.016 <br>

<a name="8"></a><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3324515/">[8]</a> Schulz, Marcel H et al. “Oases: robust de novo RNA-seq assembly across the dynamic range of expression levels” Bioinformatics (Oxford, England) vol. 28,8 (2012): 1086-92. <br>
