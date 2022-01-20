# Metagenomics

## Stat
https://github.com/shenwei356/seqkit

seqkit stat -j 72 *.fastq.gz

## Trimming
https://jgi.doe.gov/data-and-tools/bbtools/bb-tools-user-guide/data-preprocessing/

https://jgi.doe.gov/data-and-tools/bbtools/bb-tools-user-guide/bbduk-guide/

http://seqanswers.com/forums/showthread.php?t=42776


\# To get and save help and options of bbduk.sh, run

\# /home/user/Programs/bbmap/bbduk.sh > bbduk_help.txt

\# Download "bbduk_help.txt" and open with Notepad++


### (First) adapter, quality, and length
/home/user/Programs/bbmap/bbduk.sh -Xmx400g \
 in1=XXX_1.fastq.gz in2=XXX_2.fastq.gz \
 out1=XXX.trim.1.fastq.gz out2=XXX.trim.2.fastq.gz \
 ref=/home/user/Programs/bbmap/resources/adapters.fa \
 ktrim=r k=23 mink=11 hdist=1 tpe tbo qtrim=rl trimq=10 minlen=100 t=72

### (Second) phiX174 decontamination
/home/user/Programs/bbmap/bbduk.sh -Xmx400g \
 in1=XXX.trim.1.fastq.gz in2=XXX.trim.2.fastq.gz \
 out1=XXX.final.1.fastq.gz out2=XXX.final.2.fastq.gz outm=XXX.phiX.fastq.gz \
 ref=/home/user/Programs/bbmap/resources/phix174_ill.ref.fa.gz \
 k=31 hdist=1 stats=XXX.phiX.stats.txt t=72

\# I have little experience with phiX174 decontamination (not so important for isolate genome, but may be important for metagenomes)

\# I don't know whether or not we can combine the above two steps into one run

## Assembly
/home/kangin/Programs/SPAdes-3.15.3-Linux/bin/spades.py --meta -1 XXX.final.1.fastq.gz -2 XXX.final.2.fastq.gz \
 -k 21,33,55,77,99,127 -m 450 -t 72 -o XXX.SPAdes
 
 
 
