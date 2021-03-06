# Containers

Our main container is designed using Bioconda to install all tools used in Sarek:
- [sarek](#sarek-)

For annotation, the main container can be used, but the cache has to be downloaded, or additional containers are available with cache (see [annotation guide](ANNOTATION.md)):
- For GRCh37:
  - [snpeffgrch37](#snpeffgrch37-)
  - [vepgrch37](#vepgrch37-)
- For GRCh38:
  - [snpeffgrch38](#snpeffgrch38-)
  - [vepgrch38](#vepgrch38-)

## What is actually inside the containers

### sarek [![sarek-docker status][sarek-docker-badge]][sarek-docker-link]

- Based on `nfcore/base:latest`
- Contain **[AlleleCount][allelecount-link]** 2.1.2
- Contain **[BCFTools][bcftools-link]** 1.9
- Contain **[BWA][bwa-link]** 0.7.17
- Contain **[FastQC][fastqc-link]** 0.11.8
- Contain **[FreeBayes][freebayes-link]** 1.2.0
- Contain **[GATK4][gatk4-link]** 4.1.1.0
- Contain **[GeneSplicer][genesplicer-link]** 1.0
- Contain **[HTSlib][htslib-link]** 1.9
- Contain **[IGVtools][igvtools-link]** 2.3.93
- Contain **[Manta][manta-link]** 1.5.0
- Contain **[MultiQC][multiqc-link]** 1.7
- Contain **[Qualimap][qualimap-link]** 2.2.2b
- Contain **[R][r-link]** 3.5.1
- Contain **[RColorBrewer][rcolorbrewer-link]** 1.1
- Contain **[Rtracklayer][rtracklayer-link]** 1.42.1
- Contain **[samtools][samtools-link]** 1.9
- Contain **[snpEff][snpeff-link]** 4.3.1t
- Contain **[Strelka2][strelka-link]** 2.9.3
- Contain **[VCFanno][vcfanno-link]** 0.3.1
- Contain **[VCFtools][vcftools-link]** 0.1.16
- Contain **[VEP][vep-link]** 96.0

### snpeffgrch37 [![snpeffgrch37-docker status][snpeffgrch37-docker-badge]][snpeffgrch37-docker-link]

- Based on `nfcore/base:latest`
- Contain **[snpEff][snpeff-link]** 4.3.1t
- Contain cache for GRCh37.75

### snpeffgrch38 [![snpeffgrch38-docker status][snpeffgrch38-docker-badge]][snpeffgrch38-docker-link]

- Based on `nfcore/base:latest`
- Contain **[snpEff][snpeff-link]** 4.3.1t
- Contain cache for GRCh38.86

### vepgrch37 [![vepgrch37-docker status][vepgrch37-docker-badge]][vepgrch37-docker-link]

- Based on `nfcore/base:latest`
- Contain **[GeneSplicer][genesplicer-link]** 1.0
- Contain **[VEP][vep-link]** 96.0
- Contain cache for GRCh37 version 96

### vepgrch38 [![vepgrch38-docker status][vepgrch38-docker-badge]][vepgrch38-docker-link]

- Based on `nfcore/base:latest`
- Contain **[GeneSplicer][genesplicer-link]** 1.0
- Contain **[VEP][vep-link]** 96.0
- Contain cache for GRCh38 version 96

## Building

A Nextflow script is provided to build and/or push containers from Docker, or build for Singularity.

### Usage

```bash
nextflow run build.nf [--docker] [--singularity] /
[--containerPath <path>] [--push] [--containers <container1[,container2..]>] /
[--repository <repository>] [--tag tag]
```

- `--containers`: Choose which containers to build.
Default: `all`.
Possible values (to separate by commas):
  - `all` -  all available containers.
  - `sarek` - the [sarek](#sarek-) container.
  - `snpeffgrch37` - the [snpeffgrch37](#snpeffgrch37-) container.
  - `snpeffgrch38` - the [snpeffgrch38](#snpeffgrch38-) container.
  - `vepgrch37` - the [vepgrch37](#vepgrch37-) container.
  - `vepgrch38` - the [vepgrch38](#vepgrch38-) container.

- `--docker`: Build containers using `Docker`
- `--push`: Push containers to `DockerHub`
- `--repository`: Build containers under given repository.
Default: `maxulysse`
- `--singularity`: Build containers using `Singularity`.
- `--containerPath`: Select where to download containers.
Default: `$PWD`
- `--tag`: Build containers using given tag.
Default is version number.

### Example

```bash
nextflow run build.nf --docker --singularity --push --containers sarek
```

### For lazy users
We provide script to build/push or pull all containers
```bash
./scripts/do_all.sh        # Build all docker containers
./scripts/do_all.sh --push # Build and push all Docker containers into DockerHub
./scripts/do_all.sh --pull # Pull all containers from DockerHub with Singularity
```

## Building your own
Most of the containers are designed using Bioconda.
The `environment.yml` file can easilly be modified if particular versions of tools are more suited to your needs.
You can then use the building script to build your own containers.
You'll just need to specify the correct repository either in command line or in the configuration files.

[allelecount-link]: https://github.com/cancerit/alleleCount
[bcftools-link]: https://github.com/samtools/bcftools
[bwa-link]: https://github.com/lh3/bwa
[fastqc-link]: http://www.bioinformatics.babraham.ac.uk/projects/fastqc/
[freebayes-link]: https://github.com/ekg/freebayes
[gatk4-link]: https://github.com/broadinstitute/gatk
[genesplicer-link]: https://ccb.jhu.edu/software/genesplicer/
[htslib-link]: https://github.com/samtools/htslib
[igvtools-link]: http://software.broadinstitute.org/software/igv/
[manta-link]: https://github.com/Illumina/manta
[multiqc-link]: https://github.com/ewels/MultiQC/
[qualimap-link]: http://qualimap.bioinfo.cipf.es
[r-link]: https://www.r-project.org/
[rcolorbrewer-link]: https://CRAN.R-project.org/package=RColorBrewer
[rtracklayer-link]: https://www.bioconductor.org/packages/release/bioc/html/rtracklayer.html
[samtools-link]: https://github.com/samtools/samtools
[sarek-docker-badge]: https://img.shields.io/docker/automated/maxulysse/sarek.svg
[sarek-docker-link]: https://hub.docker.com/r/maxulysse/sarek
[snpeff-link]: http://snpeff.sourceforge.net/
[snpeffgrch37-docker-badge]: https://img.shields.io/docker/automated/maxulysse/snpeffgrch37.svg
[snpeffgrch37-docker-link]: https://hub.docker.com/r/maxulysse/snpeffgrch37
[snpeffgrch38-docker-badge]: https://img.shields.io/docker/automated/maxulysse/snpeffgrch38.svg
[snpeffgrch38-docker-link]: https://hub.docker.com/r/maxulysse/snpeffgrch38
[strelka-link]: https://github.com/Illumina/strelka
[vcfanno-link]: https://github.com/brentp/vcfanno
[vcftools-link]: https://vcftools.github.io/index.html
[vep-link]: https://github.com/Ensembl/ensembl-vep
[vepgrch37-docker-badge]: https://img.shields.io/docker/automated/maxulysse/vepgrch37.svg
[vepgrch37-docker-link]: https://hub.docker.com/r/maxulysse/vepgrch37
[vepgrch38-docker-badge]: https://img.shields.io/docker/automated/maxulysse/vepgrch38.svg
[vepgrch38-docker-link]: https://hub.docker.com/r/maxulysse/vepgrch38
