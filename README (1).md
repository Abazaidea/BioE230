
# BioE 230 Week 3 - Data Wrangling 

Go to the NCBI Dataset website (https://www.ncbi.nlm.nih.gov/datasets/) and find every complete bacterial genome that was released up to or before 2001.
(Note: There should be 14 such genomes.)

Download all the genome sequences as Genome FASTA files. Download the metadata (the data table), together with the GC percentage, Contig N50, Scaffold count, and genome size in megabases.



## Question 1 

- Write a README file containing all commands you run to complete these tasks, and their output, and commit the README to a new repository on Github.

- Copy the files to your home directory on IBEX. Uncompress the zip file on IBEX.

### Copy Command 
```javascript
scp /Users/Assoor_ali/Downloads/ncbi_dataset.zip abazaiea@ilogin.ibex.kaust.edu.sa:/home/abazaiea/
```


###  Uncompress Command 
```javascript
unzip ncbi_dataset.zip

```


## Question 2
What is the smallest and what is the largest genome in the ones
you just downloaded? Write a command that outputs only the line with the smallest (largest) genome.

- Largest genome name and size 
### Command 
```javascript
cut -f 1,11 data_summary.tsv | tail -n +2 | sort -t$'\t' -n -k2 | tail -n 1

```

### Output
```javascript
Vibrio cholerae O1 biovar El Tor str. N16961	4033464

```
- Smallest genome name and size 
### Command 
```javascript
cut -f 1,11 data_summary.tsv | tail -n +2 | sort -t$'\t' -n -k2 | head -n 1

```

### Output
```javascript
Chlamydia trachomatis D/UW-3/CX     1042519

```
#### Comments: 
The (sort -t$'\t' -n -k2) command sorts data based on the second column, treating the values as numbers, and considers tab characters as field separators. It was taught to me by my classmate Omar. 

### Expand your command to output only the genome size.
- Largest genome size 
### Command 
```javascript
cut -f 1,11 data_summary.tsv | tail -n +2 | sort -t$'\t' -n -k2 | tail -n 1 | awk '{print $NF}'

```

### Output
```javascript
4033464

```

- Smallest genome size 
### Command 
```javascript
cut -f 1,11 data_summary.tsv | tail -n +2 | sort -t$'\t' -n -k2 | head -n 1 | awk '{print $NF}'

```

### Output
```javascript
1042519
```

#### Comments: 
The (awk '{print $NF}') command sreads input line by line and prints the last field of each line. If fields are separated by whitespace (the default behavior), it will output the last word or value of each line. It was taught to me by my classmate Omar to be able to output only the size. 
## Question 3
Find the number of genomes that contain at least two “c” in
the species name. Your command should be a single line and output a number.

### command 
```javascript
cut -f 1 ncbi_dataset.tsv | tail -n +2 | uniq |  grep -ic 'c.*c'

``` 

### output
```javascript
7

```

### How many of the species names contain two or more “c” but do not contain the word “coccus”?

### command 
```javascript
cut -f 1 ncbi_dataset.tsv | tail -n +2 | uniq |  grep -io 'c.*c' | grep -ivc 'coccus'

```

### output
```javascript
5

```
## Question 4
Use the find command to find all genome files (FASTA) larger than 3 megabyte. How many are there (output only the number).

### command 
```javascript
find . -type f -size +3M | wc -l

```

### output
```javascript
6

```
#### Comments: 
I got 6 as the answer because it's counting for GCA and GCF files since I have both in my folder. 