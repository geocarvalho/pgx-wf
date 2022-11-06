# Data accesss
- [1000 Genomes 30x on GRCh38](https://www.internationalgenome.org/data-portal/data-collection/30x-grch38)
- Download [TSV](https://www.ebi.ac.uk/ena/browser/view/PRJEB31736) to select NA12878 cram file for download
```bash
$ grep NA12878 filereport_read_run_PRJEB31736_tsv.txt | grep cram
$ mkdir NA12878
# If you want to download all the bam file, if not check "Transform CRAM to BAM"
$ time wget ftp.sra.ebi.ac.uk/vol1/run/ERR323/ERR3239334/NA12878.final.cram data/NA12878
```

## Download reference genome
```bash
$ mkdir ref
$ time wget ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/GRCh38_full_analysis_set_plus_decoy_hla.fa data/ref
$ time wget ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/GRCh38_full_analysis_set_plus_decoy_hla.fa.fai data/ref
```

## Build images
```bash
$ cd tools/samtools
$ docker build . -t samtools:1.16.1
```

## Transform CRAM to BAM (only chromossome 22 for CYP2D6 study)
```bash
$ cd ../../data/
$ docker run -v $PWD:/data samtools:1.16.1 samtools view -b \
    --reference /data/ref/GRCh38_full_analysis_set_plus_decoy_hla.fa \
    ftp://ftp.sra.ebi.ac.uk/vol1/run/ERR323/ERR3239334/NA12878.final.cram chr22 > NA12878/NA12878.chr22.bam
$ docker run -v $PWD:/data samtools:1.16.1 samtools index /data/NA12878/NA12878.chr22.bam
```

## References
- [Informatics on High-Throughput Sequencing Data Module 5 Lab](https://bioinformaticsdotca.github.io/HTG_2021/CBW_HTseq_module5/index.html)