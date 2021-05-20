# Creat annotation database for Annovar

The guide describes the process of generating a database file and associated index file for [Annovar] - an 
annotation tool.

## Requirements
1. Annotation file with specific data columns
2. A [Perl] script from the [Annovar Author] (**Note:** You can ask the [Annovar Author] to provide the index script.)

## Annotation file formats
The annotation file must be in the tab-delimited (TXT/TSV) format.

### Important Notes
1. The annotation file may contain the header line as a first line that starts with `#`.
2. For `region based` annotation, it is recommended to use the `BED` file.

### Region-based annotation file specification
Following are the required columns to present in the annotation file.
* Chromosome (e.g. chr1 or 1)
* Start
* End
* annotation columns

### Gene-based annotation file specification
Following are the required columns to present in the annotation file.
* Chromosome (e.g. chr1 or 1)
* Start
* End
* gene name
* other annotation columns

### Filter-based annotation file specification
Following are the required columns to present in the annotation file.
* Chromosome (e.g. chr1 or 1)
* Start
* End
* Ref
* Alt
* annotation columns

## How to create custom annovar database index (Davelab only)?
Follow the steps listed below to create database index file:

1. Start the [GCP] instance named `tushar-annovar-hg38`
2. `SSH` to the instance
3. Change the directory to `annovar` directory

```bash
$ cd /ref/annovar
```

4. Copy the annotation file in the `humnadb dir`
5. Run the index script

```bash
# replace the annotation file name with the respective file name in the command line below
$ perl compileAnnnovarIndex.pl humandb/annotation.txt 1000 > humandb/hg38_annotation.txt
```

6. Test the added new annotation database with the command line below:

```bash
# Please use the annotation file name excluding the build version and extension
# (e.g. hg38_refgene.txt ==> refgene)
# gene-based annotation test
perl table_annovar.pl sample.vcf humandb --vcfinput --remove --buildver hg38 --outfile annotated_sample.vcf --protocol 
gene_based_annotation_file_name --operation g --nastring .

# region-based annotation test
perl table_annovar.pl sample.vcf humandb --vcfinput --remove --buildver hg38 --outfile annotated_sample.vcf --protocol 
region_based_annotation_file_name --operation r --nastring .

# function-based annotation test
perl table_annovar.pl sample.vcf humandb --vcfinput --remove --buildver hg38 --outfile annotated_sample.vcf --protocol 
function_based_annotation_file_name --operation f --nastring .
```

[Annovar]:https://annovar.openbioinformatics.org/en/latest/
[Perl]:https://www.perl.org/
[Annovar Author]:<mailto:kaichop@gmail.com>
[GCP]:https://cloud.google.com/
