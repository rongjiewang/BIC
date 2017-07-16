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
[kmer count options]
*       -in                              (1 arg) :    reads file
*       -kmer-size                       (1 arg) :    size of a kmer  [default '31']
*       -abundance-min                   (1 arg) :    min abundance threshold for solid kmers  [default '3']
*       -abundance-max                   (1 arg) :    max abundance threshold for solid kmers  [default '2147483647']
*       -abundance-min-threshold         (1 arg) :    min abundance hard threshold (only used when min abundance is "auto")  [default '3']
*       -histo-max                       (1 arg) :    max number of values in kmers histogram  [default '10000']
*       -solidity-kind                   (1 arg) :    way to compute counts of several files (sum, min, max, one, all)  [default 'sum']
*       -max-memory                      (1 arg) :    max memory (in MBytes)  [default '5000']
*       -max-disk                        (1 arg) :    max disk   (in MBytes)  [default '0']
*       -solid-kmers-out                 (1 arg) :    output file for solid kmers (only when constructing a graph)  [default '']
*       -out                             (1 arg) :    output file  [default '']
*       -out-dir                         (1 arg) :    output directory  [default '.']
*       -out-tmp                         (1 arg) :    output directory for temporary files  [default '.']
*       -out-compress                    (1 arg) :    output compression level (0:none, 9:best)  [default '0']

   [kmer count, advanced (developer) options]
*          -minimizer-type   (1 arg) :    minimizer type (0=lexi, 1=freq)  [default '0']
*          -minimizer-size   (1 arg) :    size of a minimizer  [default '8']
*          -repartition-type (1 arg) :    minimizer repartition (0=unordered, 1=ordered)  [default '0']
*       e                (0 arg) :    for encode
*       d                (0 arg) :    for decode
*       -nb-cores         (1 arg) :    nb cores  [default '0']
*       -verbose          (1 arg) :    verbosity  [default '1']


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
