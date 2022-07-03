### How to run RiboTaper:
First, create the annotation files   
Second, find the offset/cutoff for the P-site position (Obtain from Ribo-seQC)  
Third, run RiboTaper for ORF discovery 

```
# Step 1
SOFTWARE=/mnt/research/riboplant/Software/RiboTaper_v1.3/scripts
GTF=/mnt/home/larrywu/ABA/20181206/reference/Araport11_20181206.gtf
FASTA=/mnt/research/riboplant/Reference/TAIR10_chr_all_2.fas #Watch out how the chromosome number is named! Here is 0, 1, 2, ...
OUTPUT=/mnt/home/larrywu/Kyle_CTRL/analysis_Araport11_1st+2nd_Riboseq/RiboTaper_annotation
BEDTOOL=/mnt/home/larrywu/Software/bedtools_dir

#Run create_annotations_files.bash
$TAPER/create_annotations_files.bash $GTF $FASTA false false $OUTPUT $BEDTOOL $TAPER/
```

```
# Step 3
# Run on server or cluster
# Use the right version of R (and R packages) and bedtools
TAPER=/mnt/research/riboplant/Software/RiboTaper_v1.3/scripts
RNA=/mnt/home/larrywu/Kyle_CTRL/analysis_Araport11_1st+2nd_Riboseq/STAR1/RNA_CTRL_merged
RIBO=/mnt/home/larrywu/Protocol_Riboseq/data/STAR/ribo
ANNO=/mnt/home/larrywu/Kyle_CTRL/analysis_Araport11_1st+2nd_Riboseq/RiboTaper_annotation
BED=/mnt/home/larrywu/Software/bedtools_dir
OUTPUT=/mnt/home/larrywu/Protocol_Riboseq/data/RiboTaper_NEB1

# Run Ribotaper.sh
$TAPER/Ribotaper.sh $RIBO/star_riboAligned.sortedByCoord.out.bam $RNA/star_RNA_Aligned.sortedByCoord.out.bam $ANNO 24,25,26,27,28 8,9,10,11,12 $TAPER $BED 8
```

### RiboTaper ORFs_max_filt file column information:
```
gene_id<-gene id based on the annotation used
gene_symbol<-gene name based on the annotation used
transcript_id<-transcript id based on the annotation used
annotation<-gene biotype based on the annotation used
length<-length of the transcript
strand<-gene in the forward or reverse orientation
n_exons<-n of exons in the transcript
P_sites_sum<-Total sum of P-sites position mapped to the transcript
RNA_sites<-Total sum of RNA-sites position mapped to the transcript
Ribo_cov_aver<-Average coverage by all Ribo-seq reads on the transcript
RNA_cov_aver<-Average coverage by all RNA-seq reads on the transcript
category<-ORF category
ORF_id_tr<-ORF id with transcript coordinates
start_pos<-ORF start position (transcript coordinates)
stop_pos<-ORF stop position (transcript coordinates)
annotated_start<-Annotated ORF start position (transcript coordinates)
annotated_stop<-Annotated ORF stop position (transcript coordinates)
ORF_id_gen<-ORF id with genomic coordinates
ORF_length<-ORF length
ORF_P_sites<-Total sum of P-sites position mapped to the ORF
ORF_Psit_pct_in_frame<-Percentage of P-sites position mapped in frame
ORF_RNA_sites<-Total sum of RNA-sites position mapped to the ORF
ORF_RNAsit_pct_in_frame<-Percentage of RNA-sites position mapped in frame
ORF_pval_multi_ribo<-P-value for the multitaper test on the ORF region using P-sites positions
ORF_pval_multi_rna<-P-value for the multitaper test on the ORF region using RNA-sites positions
ORF_id_tr_annotated<-ORF id with annotated transcript coordinates
n_exons_ORF<-n of exons in the ORF
pct_covered_onlymulti_ribo<-percentage of the ORF region only supported by multimapping Ribo-seq reads
pct_covered_onlymulti_rna<-percentage of the ORF region only supported by multimapping RNA-seq reads
header_tofasta<-header used in the generated protein fasta file
ORF_pept<-peptide sequence of the identified ORF
```
