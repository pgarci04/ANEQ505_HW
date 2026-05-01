Beginning by... making directories with their respective files...
- attaching within metadata, the metadata text and barcodes
- And the reverse, forward, and barcodes of the data

Starting..
`ainteractive --ntasks=6 --time=04:00:00
`module purge
`module load qiime2/2026.1_amplicon

Importing sequence reads into my respective directories...
`qiime tools import \--type EMPPairedEndSequences \--input-path raw_reads_oxycow \--output-path oxycow_reads.qza`

- command went through :)), remember the output of the reads is not in a folder...

*Demultiplex*

A job was submitted in my demux... and then there's this code to run

`qiime demux emp-paired \--m-barcodes-file ../metadata/oxycow_barcodes.txt --m-barcodes-column Barcode \--p-rev-comp-mapping-barcodes \--p-rev-comp-barcodes \--i-seqs ../oxycow_reads.qza \--o-per-sample-sequences demux_oxycow.qza \--o-error-correction-details oxycow_demux_error.qza`

then you visualize
`#visualize the read quality:
`qiime demux summarize \--i-data demux_oxycow.qza \--o-visualization demux_oxycow.qzv`

Submit a job??

`#!/bin/bash
`#SBATCH --job-name=demux
`#SBATCH --nodes=1
`#SBATCH --ntasks=12
`#SBATCH --partition=amilan
`#SBATCH --time=02:00:00
`#SBATCH --mail-type=ALL
`#SBATCH --output=slurm-%j.out
`#SBATCH --qos=normal
`#SBATCH --mail-user=pgarci58@colostate.edu

`# Activate Qiime2
`module purge
`module load qiime2/2026.1_amplicon`

``# Importing qiime2 sequences
```
qiime demux emp-paired \--m-barcodes-file ../metadata/oxy_barcodes_clean2.txt --m-barcodes-column Barcode \--p-rev-comp-mapping-barcodes \--p-rev-comp-barcodes \--i-seqs ../oxycow_reads.qza \--o-per-sample-sequences demux_oxycow.qza \--o-error-correction-details oxycow_demux_error.qza

`#visualize the read quality
`qiime demux summarize \--i-data demux_oxycow.qza \--o-visualization demux_oxycow.qzv`

To submit...
`dos2unix demux.sh
 `sbatch demux.sh`
- Job failed, based off Catie's notes it with the sample ID names with "/"

Checking to see those with "/"
`head oxy_barcodes.txt

clean copy
awk 'BEGIN{FS=OFS="\t"} 
NR==1 {print; next} 
{
  gsub(/\//, "_", $1)
  gsub(/:/, "_", $1)
  gsub(/ /, "", $1)
  print
}' oxy_barcodes.txt > oxy_barcodes_clean.txt
```


cd dada2
Denoise
- Rename for the metadata sections and the barcode clean text.
```
qiime dada2 denoise-paired \--i-demultiplexed-seqs ../demux/demux_oxycow.qza \--p-trim-left-f 0 \--p-trim-left-r 0 \--p-trunc-len-f 250 \--p-trunc-len-r 150 \--p-n-threads 6 \--o-representative-sequences cow_seqs_dada2.qza \--o-denoising-stats cow_dada2_stats.qza \--o-table cow_table_dada2.qza
```

- Visual...
```
qiime metadata tabulate \--m-input-file cow_dada2_stats.qza \--o-visualization cow_dada2_stats.qzv

qiime feature-table summarize \--i-table cow_table_dada2.qza \--m-sample-metadata-file ../metadata/oxycow_metadata_final.txt \--o-visualization cow_table_dada2.qzv

qiime feature-table tabulate-seqs \--i-data cow_seqs_dada2.qza \--o-visualization cow_seqs_dada2.qzv
```