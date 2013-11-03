#iTree: phylogenomic pipeline

##Phylogenomics
[Phylogenomics](http://en.wikipedia.org/wiki/Phylogenomics), conventionally defined as the intersection of phylogenetics and genomics, has become a key instrument in a wide spectrum of biological studies, including resolution of complex evolutionary relationships, assignment of taxonomic affiliation, prediction of protein molecular functions, and tracing horizontal gene transfer event. iTree automates the execution of phylogenetic analyses under multithreaded or grid-computing environments, providing a scalable high-throughput platform for performing genome-wide evolutionary analyses.
##Databases
A key step in a [phylogenetic analysis](http://en.wikipedia.org/wiki/Phylogenetics) is collecting homologous sequences to the query of interest. This step is typically done through a [BLAST](http://en.wikipedia.org/wiki/BLAST) search against a database. The content of the database has a direct on the taxon sampling and the phylogeny to be inferred. To maximize the sampling, iTree uses the results of BLAST against NBCI [RefSeq](http://www.ncbi.nlm.nih.gov/refseq/) for protein phylogenies and [SILVA](http://www.arb-silva.de/) for ribosomal RNA (rRNA) phylogenies. In both cases, there are the BLAST-formatted (via [formatdb](ftp://ftp.ncbi.nih.gov/blast/documents/formatdb.html) on a [FASTA-formatted](http://en.wikipedia.org/wiki/FASTA_format) file) database and a corresponding [relational database](http://en.wikipedia.org/wiki/Relational_database).
###RefSeq
To make the tree more readable in terms of taxonomic information, the sequences in RefSeq are renamed in the iTree version. The adopted naming convention is `domain.group.genus_species-txid_gi`, where:

Token     | Description
--------- | -----------
`domain`  | `A` : Archaea, `B` : Bacteria, `E` : Eukarya, `V` : Vira (Viruses)
`group`   | Basically a major taxonomic under the specific domain
`genus`   | Genus name
`species` | Species (or strain) name
`txid`    | NCBI [taxon identifier](http://www.ncbi.nlm.nih.gov/taxonomy)
`gi`      | NCBI [gi number](http://www.ncbi.nlm.nih.gov/Sitemap/sequenceIDs.html)

Although, this naming convention produces pretty long names (the average name length is 66 characters), it makes much easier to recognize the taxonomic classification and the relationship between lineages in a phylogenetic tree even for non-taxonomists.

The renamed RefSeq protein sequences are stored as Fasta for BLAST and MySQL (at least for now) for fast access and retrieval.

Because of a GitHub limitation on the size of files to be pushed to repositories (for more information, see [Working with large files](https://help.github.com/articles/working-with-large-files) and [What is my disk quota?](https://help.github.com/articles/what-is-my-disk-quota)), the iTree databases have been deployed to [Sourceforge](http://sourceforge.net/projects/itree/files/).

The current versions based on the [RefSeq Release 61 (September 2013)](ftp://ftp.ncbi.nlm.nih.gov/refseq/release/release-notes/RefSeq-release61.txt) can be downloaded from [here](http://sourceforge.net/projects/itree/files/refseq_rel_61/).

Database File | Description | Size
------------- | ----------- | ----
`itree_refseq_61.fas.bz2` | Fasta sequences | 6.5 GB 
`itree_refseq_61.sql.bz2` | MySQL dump | 6.8 GB

After downloading, to load the MySQL dump
```
$ bzip2 -d itree_refseq_61.sql.bz2
$ mysqladmin -u root -p create itree
$ mysql -u root -p < itree_refseq_61.sql
```

Given the large size of the dump (> 20 GB uncompressed), the last step takes quite some time, varying according to the power of the host machine. For example, on an [Amazon EC2 medium instance](http://aws.amazon.com/ec2/instance-types/instance-details/), doing nothing else, it takes about 12 hours!

Generally, these databases (Fasta and MySQL) can be utilized independently of iTree. They might be plugged into other phylogenomic pipelines or other general purpose usage.

###SILVA
Coming soon...


##Citation
Moustafa, A., Bhattacharya, D., and Allen, A.E. (2010). iTree: A high-throughput phylogenomic pipeline. Biomedical Engineering Conference (CIBEC), 2010 5th Cairo International, pp. 103–107.

DOI [10.1109/CIBEC.2010.5716071](http://dx.doi.org/10.1109/CIBEC.2010.5716071)
