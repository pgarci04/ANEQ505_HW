Beginning by... making directories with their respective files...
- attaching within metadata, the metadata text and barcodes

Starting..
`ainteractive --ntasks=6 --time=04:00:00
`module purge
`module load qiime2/2026.1_amplicon

Importing sequence reads into my respective directories...
`qiime tools import \--type EMPPairedEndSequences \--input-path raw_reads_oxycow \--output-path oxycow_reads.qza`

