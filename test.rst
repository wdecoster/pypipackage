Nanofilt
========

Filtering and trimming of Oxford Nanopore sequencing data.

| Filtering on quality and/or read length, and optional trimming after
  passing filters.
| Reads from stdin, writes to stdout.

Intended to be used: - directly after fastq extraction - prior to
mapping - in a stream between extraction and mapping

| See also `my post about NanoFilt on my blog Gigabase or
  gigabyte <https://gigabaseorgigabyte.wordpress.com/2017/06/05/trimming-and-filtering-oxford-nanopore-sequencing-reads/>`__.
| Due to `a
  discrepancy <https://gigabaseorgigabyte.wordpress.com/2017/07/14/calculated-average-quality-vs-albacore-summary/>`__
  between calculated read quality and the quality as summarized by
  albacore this script takes since v1.1.0 optionally also a
  ``--summary`` argument. Using this argument with the
  sequencing\_summary.txt file from albacore will do the filtering using
  the quality scores from the summary. It's also faster.

INSTALLATION AND UPGRADING:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    pip install nanofilt
    pip install nanofilt --upgrade

NanoFilt is written for Python 3, but should also work for python2.7.

USAGE:
~~~~~~

::

    usage: NanoFilt [-h] [-q QUALITY] [-l LENGTH] [--headcrop HEADCROP] [--tailcrop TAILCROP]

    optional arguments:  
      -h, --help            show this help message and exit  
      -s --summary SUMMARYFILE optional, the sequencing_summary file from albacore for extracting quality scores
      -q, --quality QUALITY  Filter on a minimum average read quality score  
      -l, --length LENGTH Filter on a minimum read length  
      --headcrop HEADCROP   Trim n nucleotides from start of read  
      --tailcrop TAILCROP   Trim n nucleotides from end of read

Example:

.. code:: bash

    zcat reads.fastq.gz | NanoFilt -q 10 -l 500 --headcrop 50 | bwa mem -t 48 -x ont2d genome.fa - | samtools sort -O BAM -@24 -o alignment.bam -
    zcat reads.fastq.gz | NanoFilt -q 12 --headcrop 75 | gzip > trimmed-reads.fastq.gz
    zcat reads.fastq.gz | NanoFilt -q 10 | gzip > highQuality-reads.fastq.gz
