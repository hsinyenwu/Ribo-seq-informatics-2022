## Calculate in-frame percentage (a.k.a. 3-nt periodicity) for CDS region

In this case, we calculated the 3-nt periodicity for 28 nucleotide (length) reads. The figure below is from Ribo-seQC output.  

<img width="594" alt="image" src="https://user-images.githubusercontent.com/4383665/177381417-2645ae2e-f6ab-4c6c-9ac4-b43df382900c.png">

The blue box marks the region for our 3-nt periodicity calculation:
<img width="603" alt="image" src="https://user-images.githubusercontent.com/4383665/177381221-815e36db-045e-4a24-9bbf-7e30e2deeb77.png">


The -1 codon from stop codon usually has a high peak at the second nucleotide (see **green** peak below). The figure below is from Ribo-seQC output.  
<img width="145" alt="image" src="https://user-images.githubusercontent.com/4383665/173270154-df8d6cee-e669-435f-a569-3fc003398865.png">

```
# Load the results_RiboseQC file from Ribo-seQC output
load("~/Desktop/New_Riboseq/NEB_STAR_out/star_ribo_NEB3Aligned.sortedByCoord.out.bam_results_RiboseQC")
# Extract P_sites_subcodon
P_sites_subcodon_readCount = res_all[["profiles_P_sites"]][["P_sites_subcodon"]][["nucl"]][["28"]]
# Print out P_sites_subcodon_readCount
P_sites_subcodon_readCount

# Get the CDS region
P_CDS = P_sites_subcodon_readCount[51:149] #93 nt total, 33 nt start and after, 33 nt in the middle, 27 nt from -2 codon of stop codon to -11 codon of stop codon

# Get total number of reads for 3 frames
F1 = sum(P_CDS[seq(1,93,by=3)])
F2 = sum(P_CDS[seq(2,93,by=3)])
F3 = sum(P_CDS[seq(3,93,by=3)])
F1/(F1+F2+F3)*100 #[1] 91.03305
```


#### Note:
Ribo-seQC provides a value called **"frame preference"**. This value is the in-frame percentage in the blue box below:
<img width="627" alt="image" src="https://user-images.githubusercontent.com/4383665/173368221-3d5ba715-53ae-4d9a-bc0d-5a03af1e4ced.png">  
Please note this plot starts differently than the plot shown above. This plot and the frame preference are used for determine the cutoff value for different lengths of Ribo-seq reads. Frame preference gives you an idea about periodicity, but (1) it could miss the front area with high periodicity (2) included the last codon before stop, which has a signiture peak at the 2nd nucleotide. Therefore, frame preference is usually lower than 3nt periodicity calculated above.


