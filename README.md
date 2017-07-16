#About BIC
BIC - A bucket index correction based method for compression of genomic sequencing data.

https://github.com/rongjiewang/BIC.git

This is a software tool relying on GATB-CORE library, reads error correction tool Bloocoo and compression tool ORCOM.

The executable files of the tool is as follows:

    * BIC_b - bucketing corrected reads into buckets.
    * BIC_c - compressing each bucket with PPMd method.

# Usage

## BIC_b
### Command line
BIC_b is run from the command prompt:

    BIC_b <e|d> [options]

in one of the two modes:
* `e` - encoding,
* `d` - decoding,

with available options:
* `-i<file>` - input file,
* `-f"<f1> <f2> ... <fn>"` - input file list,
* `-g` - input compressed in `.gz` format,
* `-o<f>` - output files prefix,
* `-p<n>` - signature length, default: `8`,
* `-s<n>` - skip-zone length, default: `12`,
* `-b<n>` - FASTQ input buffer size (in MB), default: `256`,
* `-t<n>` -  worker threads number, default: `8`,
* `-v` - verbose mode, default: `false`.

### Examples

Encode (cluster) reads from `input.fastq` file.

    BIC_b e -in input.fastq -out bucketFile
Decode reads from `bucketFile` bucket files and save the DNA reads to `decode.dna` file.

    BIC_b d -in bucketFile -out decode.dna




## BIC_c
### Command line
BIC_c is run from the command prompt:

    BIC_c <e|d> [options]

in one of the two modes:
* `e` - encoding,
* `d` - decoding,

with available options:
*	-i<file>	: BIC_c generated input files prefix
*	-o<file>	: output files prefix
*	-e<n>		: encode threshold value, default: 0 (0 - auto)
*	-m<n>		: mismatch cost, default: 2
*	-s<n>		: insert cost, default: 1
*	-t<n>		: threads count, default: 8
*	-v		: verbose mode, default: false

### Examples

Encode (compress) clustered reads from `bucketFile` bucket files and save the output to `compressedFile` archive files:

    BIC_c e -ibucketFile -ocompressedFile
Decode reads from `compressedFile` archive files and save the DNA reads to `decode.dna` file.

    BIC_c d -icompressedFile -odecode.dna
