## Calculate 3nt periodicity for CDS region

```
load("~/Desktop/New_Riboseq/NEB_STAR_out/star_ribo_NEB3Aligned.sortedByCoord.out.bam_results_RiboseQC")
B=res_all[["profiles_P_sites"]][["P_sites_subcodon"]][["nucl"]][["28"]]
B_CDS=B[51:149]
F1=sum(B_CDS[seq(1,93,by=3)])
F2=sum(B_CDS[seq(2,93,by=3)])
F3=sum(B_CDS[seq(3,93,by=3)])
F1/(F1+F2+F3)*100 #[1] 91.03305
```
