# Task name conventions

An anlytical pipeline consists of following four components:
1. Graph configuration
2. Resource configuration
3. Platform configuration
4. Sample sheet

The graph configuration includes one or more tasks and task connections. The task name solely depdends on the 
developer which results into the inconsistant task names. So, a standard naming convention implemented for every 
developer to follow.

Following is the task name convention, every developer should follow:
```bash
module_[submodule]__[functionality]__[input-from]__assay
```

The order in the above convention matters. The things in the brakets are used to remove the duplicate task names. 
The graph configuration validation fails if more than one task names are identical.

Following are the examples of the task names, please use them as reference as per you need.

## Example - 1
The task name should always start with the `CloudConductor (CC) module` name, followed by the assay name (i.e. TNA, 
DNA, RNA). I
```bash
demuxtna__tna
star__rna
trimmomatic__dna
trimmomatic__rna
```

## Example - 2
When the task contains the `CC module` and `CC submodule`, the task name should always start with `CC module name` 
(all lower letter case) followed by `CC submodule name` followed by `assay name`.
```bash
utils_consolidatesamplename__tna
utils_springdecompress__tna
utils_moveumitobamtag__rna
sentieon_bwamem__dna
```

## Example - 3
In the situation when the same `CC module` and `CC submodule` used multiple times, to remove the duplication, please 
use `functionality` in the task name.
```bash
fastqc__raw__rna
fastqc__trim__rna
picard_markduplicates__umi__dna
gatk_filtersamreads__spliced__dna
```

## Example - 4
When the `CC module`, `CC submodule`, `functionality` can not resolve the task name duplication, please use the 
`parent task name`.
```bash
samtools_index__utils_moveumitobamtag__rna
samtools_index__picard_markduplicates__umi__rna
samtools_index__utils_moveumitobamtag__dna
samtools_index__picard_markduplicates__umi__dna
```

If you have any question about the `task name` conventions, please contact [Tushar Dave](mailto:tushar.dave@duke.edu). 

