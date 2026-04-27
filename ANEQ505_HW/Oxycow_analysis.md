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

A job was submitted in my demux... and then there's this code to

`qiime demux emp-paired \--m-barcodes-file ../metadata/oxycow_barcodes.txt --m-barcodes-column Barcode \--p-rev-comp-mapping-barcodes \--p-rev-comp-barcodes \--i-seqs ../oxycow_reads.qza \--o-per-sample-sequences demux_oxycow.qza \--o-error-correction-details oxycow_demux_error.qza`
