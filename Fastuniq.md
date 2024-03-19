code Fastuniq- input/output files

```
for i in $(seq 43 47); do /home/minerva/Documents/Software/FastUniq/source/fastuniq -i /home/minerva/Documents/Tutorial1+2/RequieredFiles/fastuniqInput_${i}.txt -o  /home/minerva/Documents/Tutorial1+2/Output/WGS/fastUnique_ex2/${i}R1_fastQ -p /home/minerva/Documents/Tutorial1+2/Output/WGS/fastUnique_ex2/${i}R2_fastQ; done
```

code Trimmomatic- seq. adaptors removing 

![ph](https://github.com/orarg/population-genomic/blob/main/Slides/Screenshot%202024-03-18%20145912.png)


```
for i in $(seq 43 47) ;           
do
java -jar ~/Documents/Software/Trimmomatic-0.39/trimmomatic-0.39.jar PE -phred33 -trimlog ~/Documents/Tutorial1+2/Output/WGS/Trimmomatic/trimlog.log ~/Documents/Tutorial1+2/Output/WGS/fastuniq/${i}_R1.fastq ~/Documents/Tutorial1+2/Output/WGS/fastuniq/${i}_R2.fastq -baseout ~/Documents/Tutorial1+2/Output/WGS/Trimmomatic/trim_${i}.fastq.gz ILLUMINACLIP:~/Documents/Software/Trimmomatic-0.39/adapters/TruSeq3-PE-2.fa:2:30:10:8:true SLIDINGWINDOW:4:15 MINLEN:80
done
```

code- fastqc Illumina reades quality (confirm that trimmomatic removed the adaptor contamination)

```
for i in $(seq 43 47); do fastqc ~/Documents/Tutorial1+2/Output/WGS/Trimmomatic/trim_${i}*.fastq.gz; done
```

*= ignor the rest of the file name after the *. (P=paird , U= unpaird)


*Working with VCF file*

The VCF ia a huge table.

![](https://github.com/orarg/population-genomic/blob/main/Slides/Screenshot%202024-03-19%20145537.png)

We want to sort and edit vcf files according to our needs.

In this case we look to take out the missing date from the sampled individuals:

```
~/Documents/Software/vcftools_0.1.13/bin/vcftools --vcf ~/Documents/Tutorial1+2/RawData/RAD/vcf_filt.recode.vcf --missing-indv --out ~/Documents/Tutorial1+2/Output/RAD/VCFTools/MissingIndv

--vcf input file
--missing-indv flag
--out 
```

After finding the missing data we want to sort the indeviduals which are missing data:

```
sort -k 4 -n MissingIndv.imiss > MissingIndvSorted.imiss
```

We put this file back to VCF tool and we ask the tool to take out the indeviduals with missing data:

```
/Documents/Software/vcftools_0.1.13/bin/vcftools --vcf ~/Documents/Tutorial1+2/RawData/RAD/vcf_filt.recode.vcf --remove-indv ~/Documents/Tutorial1+2/RequieredFiles/missingSamples.txt --recode --out ~/Documents/Tutorial1+2/Output/RAD/VCFTools/removedIndv

--vcf input filename
--remove-indv sample list or individual sample ID
--recode flag to get a vcf output
--out output filename
```

In our case of the data the best indevidual missing the 30% of the SNPs, the worste one is missint 97%. 

We should plot the data and see what is the data looks like to make a deccision on my sampling.

The plot of the data:


![](https://github.com/orarg/population-genomic/blob/main/Slides/Screenshot%202024-03-19%20145523.png)


Last column in the VCF is the "%_of_Missing"

What is the SNPs depht per site:

```
We will also remove loci that have too high depth. These are indicative of errors in assembly of the reference, where duplicated regions might be misassembled. To do this we will plot the site mean depth:
~/Documents/Software/vcftools_0.1.13/bin/vcftools --vcf ~/Documents/Tutorial1+2/Output/RAD/VCFTools/removedIndv.recode.vcf --site-mean-depth --out ~/Documents/Tutorial1+2/Output/RAD/VCFTools/SiteMeanDepth

--vcf input file
--site-mean-depth flag to get the mean depth per site
--out output file
```

![photo_from_slide](https://github.com/orarg/population-genomic/blob/main/Slides/Screenshot%202024-03-19%20145609.png)

Filtering the depht of coverage, 30 is alot we usualy want to go for 20.

It will keep the genotype call for ants with 30 and abouve reads in our case.


Some info about the parameters of the VCF:

 --max-missing, how much do I **allow** for a missing SNP (confusing meaning of the parameter name)

frequent allel count or frequency usage will be depending on what we want to test.

How many ants I have will set some of the bounderies of my analysis parameters.



*Working with graphs*

ggplot work with data frame, we need to have it defined as the type of the data which is correct.

When we make the plot we have to think what we do.

We need to combine the data, for that we need to check the data was not massed.
 R might be less god for that than excel.

 CchatGPT --> ask him "how do I plot this data in a violine shape...?"

 "jitter" option give the points of the data on a graph.

 Make sure to fit the way data visualized to the output you want the reader to get from it:



 https://www.nature.com/articles/s41467-020-19160-7

https://www.nature.com/articles/nmeth0910-665



