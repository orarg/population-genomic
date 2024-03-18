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
