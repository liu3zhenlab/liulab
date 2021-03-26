---
title: Examples using Bedtools

# Summary for listings and search engines
summary: Bedtools examples

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: true

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'bedtools'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- sanzhen

tags:
- demo

categories:
- Demo
---

##Bedtools applications

###Extract promoter sequences of genes

####1. Required input data

* gene bed 2 (genes.bed)
* chromosome fasta sequences
* chromosome lengths (chrs.length)
* length of promoters to be extracted

####2. Running scripts

####2.1 promoter sequences

```
bed=genes.bed
clen=chrs.length # e.g., /homes/liu3zhen/references/B73Ref4/genome/B73Ref4.length
ref=ref.fasta # e.g., /homes/liu3zhen/references/B73Ref4/genome/B73Ref4.fa
promoter_len=2000
out=genes.promoter
bedtools flank -i $bed -g $clen -l $promoter_len -r 0 -s > $out.bed
bedtools getfasta -s -fi $ref -bed $out.bed -fo ${out}.fasta
```

 ##### 2.1.1 example

1. ref.fas

```
>ref
AAAAAAAAAAAAAAAAAAAACCCCCCCCCCCCCCCCCCCCAAGGGGGGGGGGGGGGGGGG
```

2. gene.bed

   ```
   ref	20	40	a1	0.5	+
   ref	20	40	a2	0.5	-
   ```

3. ref.length

   ```
   ref	60
   ```

4. bedtools run

   ```
   bedtools flank -i gene.bed -g ref.length -l 20 -r 0 -s > gene.promoter.bed
   bedtools getfasta -s -fi ref.fas -bed gene.promoter.beer -fo gene.promoter.fas
   ```

5. result

   ```
   >ref:0-20(+)
   AAAAAAAAAAAAAAAAAAAA
   >ref:40-60(-)
   CCCCCCCCCCCCCCCCCCTT
   ```

   