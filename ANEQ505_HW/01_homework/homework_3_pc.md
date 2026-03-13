~={red}(1point)=~ for Alpha Rarefaction Plot
Run Core Metrics ~={red}(1 point; .25pts per line)=~
Make alpha diversity plots ~={red}(3points)=~
~={red}10 points=~ for the questions 

~={red}15 points total=~
------------------------------------------------------------------

Due: 

**For complete credit for this assignment, you must answer all questions and include all commands in your obsidian upload.**

------------------------------------------------------------------
**Learning Objectives**
1. Practice recording commands and editing code to match your analysis.
2. Perform alpha rarefaction and determine an appropriate sequencing depth.
3. Run core metrics, generate plots for alpha and beta diversity
--------------------------------------------------

**Cow Site Data Workflow**, part 3

Load qiime2 in a terminal session after you go into the **cow** folder

```
# Insert the two commands to activate qiime2

module purge

module load qiime2/2024.10_amplicon
```

### Alpha Rarefaction Plot ~={red}(1 point)=~
- Chose the input sequencings depths (min and max) for generating the alpha rarefaction plot: 

```
#go to the cow directory

qiime diversity alpha-rarefaction \--i-table dada2/cow_table_dada2_filtered300.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization alpha_rarefaction_curves_16S.qzv \--p-min-depth ADD MIN RAREFACTION DEPTH \--p-max-depth ADD MAX RAREFACTION DEPTH

qiime diversity alpha-rarefaction \--i-table dada2/cow_table_dada2_filtered300.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization alpha_rarefaction_curves_16S.qzv \--p-min-depth 10 \--p-max-depth 10000
```
Code went through and ran :)

### Run Core Metrics ~={red}(1 point)=~

```
qiime diversity core-metrics-phylogenetic \--i-table INSERT FILTERED TABLE HERE \--i-phylogeny INSERT FILE HERE \--m-metadata-file INSERT FILE HERE \--p-sampling-depth INSERT SEQ DEPTH HERE \--output-dir core_metrics_results

qiime diversity core-metrics-phylogenetic \--i-table dada2/table_nomitochloro_gg2_filtered300.qza \--i-phylogeny tree/tree_gg2.qza \--m-metadata-file metadata/cow_metadata.txt \--p-sampling-depth 3000 \--output-dir core_metrics_results

```
Not very sure on the phylogeny portion. Lowkey had to move things around :// But it worked.

### Visualize alpha diversity plots
- generate a plot to visualize the observed features ~={red}(1 point)=~
```
qiime diversity alpha-group-significance \--i-alpha-diversity core_metrics_results/FILENAME.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization core_metrics_results/OUTPUT-FILENAME.qzv

qiime diversity alpha-group-significance \--i-alpha-diversity core_metrics_results/observed_features_vector.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization core_metrics_results/observed_features_vector.qzv

```
Code put in and code ran slay :))
- generate a plot to visualize faith's PD ~={red}(2 points)=~
```
## insert the entire code chunk for generating this visualization 

qiime diversity alpha-group-significance \--i-alpha-diversity core_metrics_results/faith_pd_vector.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization core_metrics_results/faith_pd_vector.qzv

```
Code also worked here :)) yay


## Homework questions ~={red}(10 points)=~

1. what is the name of the file you needed to use to figure out what min and max depths to use to generate the alpha rarefaction plot? (Hint: which file contains the sequencing depths for each sample)
	1. cow_table_dada2.qzv 
2. what did you choose for the rarefaction depth (the input for core metrics -p-sampling-depth flag)? why? 
	1. 3000, because when looking at the alpha rarefaction visual I can see that at about 3,000 it begins to flatten out which lets me know that it has no longer recognized new taxa present in the read. So, this would let me know that past 3,000 it has stabilized and I can use those less than 3,000 for the diversity of the samples.
3. Which cow body location had more observed features? Which has the lowest?
	1. The body location with more observed features is of the skin samples. 
	2. Those with the lowest are the nasal samples.
4. What is the main difference between Faiths PD and Shannons alpha diversity metrics?
	1. The main difference between Faiths PD and Shannons is that Shannon does NOT use phylogeny while Faiths PD does use phylogenetic information.
5. Which diversity metrics produced by the core-metrics pipeline require phylogenetic information?
	1. Metrics that require phylogenetic information are Faiths PD, weighted and Unweighted UniFrac
6. Which two body sites have the highest Faiths PD alpha diversity?  Are the groups significantly different?
	1. The two with the highest Faiths PD are skin samples and fecal samples. And yes they are significantly different just from looking at their p values.
7. Does it seem like there are any groupings in the beta diversity? What are the groupings? 
	1. There is grouping when looking at beta diversity. The grouping appears as though skin and udder cluster together closer in the middle while fecal clusters in a side closer to axis 2 and nasal clusters on the complete opposite side of fecal. Oral however, is more dispersed between fecal and nasal.
8. Why do you think these samples are grouping together?
	1. 
9. What test can you run to determine if the groups are significantly different?
	1. 
10. What command would you use to run that test?

```
#insert command for running the test you suggest from question 7



```