## Calculate 3nt periodicity for CDS region

In this case, we calculate the 3-nt periodicity for 28 nucleotide long reads. The figure below is from Ribo-seQC output.  
<img width="839" alt="image" src="https://user-images.githubusercontent.com/4383665/173270126-6e057416-c4c7-44ab-b7b7-c1498fd2756e.png">

The code before stop codon usually have a high peak at the second nucleotide (see green peak below). The figure below is from Ribo-seQC output.  
<img width="145" alt="image" src="https://user-images.githubusercontent.com/4383665/173270154-df8d6cee-e669-435f-a569-3fc003398865.png">

```
# Load the results_RiboseQC file from Ribo-seQC output
load("~/Desktop/New_Riboseq/NEB_STAR_out/star_ribo_NEB3Aligned.sortedByCoord.out.bam_results_RiboseQC")
P_sites_subcodon_readCount=res_all[["profiles_P_sites"]][["P_sites_subcodon"]][["nucl"]][["28"]]
P_CDS=P_sites_subcodon_readCount[51:149]
F1=sum(P_CDS[seq(1,93,by=3)])
F2=sum(P_CDS[seq(2,93,by=3)])
F3=sum(P_CDS[seq(3,93,by=3)])
F1/(F1+F2+F3)*100 #[1] 91.03305
```
