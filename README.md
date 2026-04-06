# Lab_Week_13

This week will conduct two tasks. First, we will analyze the genome annotation, and then we will see if your species has been detected in environmental DNA samples. 

## Genome Annotation

Your genome annotation and associated data are in the folder `annotation/predict_results`

The first file we will look at is the `species.stats.json` file. Navigate into the predict_results folder and view that file with `cat`. 

### Question 1

Report the following statistics for your annotation 

1) **Protein coding genes** Total number of protein-coding genes reported. This is _not_ what is listed under "genes."
2) **tRNA genes** How many tRNA genes were annotated in your genome?
3) **Protein coding gene length** What is the average length of the protein-coding genes?
4) **Multi-exon genes** How many genes have at least one intron?



## Gene content

One thing we may want to know is if our yeast can grow on (aka metabolize) different carbon substrates. 

We know there are some essential enzymes needed to metabolize specific carbon sources. 

| Substrate | Gene |
|-----------|------|
|Galactose | GAL1 | 
| Glycerol | GUT1 |
|Lactose | LAC4 |
| Sucrose | SUC2 | 

We want to know, **does your yeast have these metabolism genes?**

### Gene Content Step 1 - Make a Blast Databse

We will use BLAST again for this analysis. The first step is to turn all of our predicted yeast proteins into a database. 

Substitute what is in between the < > with your proper input file and the type of data we are using. Our references are proteins, so we probably want to build a database with proteins. 

```
module load blast
makeblastdb -in <INPUT> -dbtype <prot or nucl>
```

### Gene Content Step 3 - Conduct a blast search

We have reference protein sequences for the 4 metabolic enzymes. Copy them to your current directory. 

```
cp /projects/class/binf3201_001/annotation/reference_sequences.fasta .
```

Now you can do your blast search

<INPUT> will be the same as above. This time we have set an e-value threshold 

An E-value (Expect value) threshold in BLAST defines the maximum number of hits one can expect to see by chance when searching a database of a particular size. Therefore, the closer the e-value is to zero, the better the match between the query and the subject. We set an e-value threshold of 1e-50 in this experiment. 

```
blastp -db <INPUT> -query reference_sequences.fasta -evalue 1e-50
```

### Question 2

Based on your blast results, can your yeast metabolize galactose, glycerol, lactose, or sucrose? Why or why not? 


##  Functional Annotation results

You also have a folder called `annotate_results` in your `annotation` folder. Navigate into that folder.

The file we will be analyzing is called `genome.annotations.txt`

### Functional Annotation Step 1 - ACT1

To see if the genome annotation found the ACT 1 gene, use the `grep` command to search for `ACT1` in the `annotations.txt` file.

### Question 3

Does your genome have a predicted ACT1 gene? 

### Functional Annotation Step 2 - Genome annotation total

This file includes the 10 columns, with the sequence in the 11th column. We want to visualize and analyze only the first 9 columns

First, save only the first 9 columns to a new file called `functional_annot.txt`

```
cut -f1-9 <NAME>.annotations.txt > functional_annot.txt
```

Take a look at this file using `cat` or `head`. 

Some of these proteins have no predicted function. These are labeled "hypothetical protein". We want to remove these from our file. To do that use this command

```
sed -i "/hypothetical protein/d" functional_annot.txt
```

### Question 4

How many genes in your genome have a known functional annotation?

### Question 5

Select a protein that is functionally annotated in your genome. Report the gene name, the description, and google 1 fact about that gene in yeast. 





