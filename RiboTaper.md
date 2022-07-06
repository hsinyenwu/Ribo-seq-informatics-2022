### How to run RiboTaper:
**First, create the annotation files **  

```
# Step 1

#$TAPER is the path to RiboTaper code files
#$GTF path to the GTF files
#$FASTA path to the FASTA files
#$OUTPUT path to the output folder
#$BED path to bedtools v2.17.0
#create_annotation_files.bash <gencode_gtf_file> <genome_fasta_file(indexed)> <use_ccdsid?> <use_appris?> <dest_folder> <bedtools_path> <scripts_dir>
#$TAPER/create_annotations_files.bash $GTF $FASTA false false $OUTPUT $BED $Taper
#$ANNO path to output files

#Run create_annotations_files.bash
cd $ANNO
$TAPER/create_annotations_files.bash $GTF $FASTA false false $OUTPUT $BEDTOOL $TAPER/
```

**Second, find the offset/cutoff for the P-site position (Obtain from Ribo-seQC) [See Step 5: Run Ribo-seQC](https://github.com/hsinyenwu/Ribo-seq-informatics-2022/blob/main/Analysis_pipeline.md)**  

**Third, run RiboTaper for ORF discovery **  
```
# Step 2
# Run on server or cluster
# Use the right version of R (and R packages) and bedtools
#$TAPER/Ribotaper.sh path to RiboTaper code files
#$RIBO/ribo.bam path to Ribo-seq bam file (STAR output)
#$RNA/RNA.bam path to RNA-seq bam file(STAR output)
#$ANNO path to RiboTaper annotation files
#$BED path to bedtools v2.17.0
#8 is the number of threads used 
#$OUTPUT path to output files

# Run Ribotaper.sh
cd $OUTPUT
$TAPER/Ribotaper.sh $RIBO/ribo.bam $RNA/RNA.bam $ANNO 24,25,26,27,28 8,9,10,11,12 $TAPER $BED 8
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
