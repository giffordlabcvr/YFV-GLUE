# YFV-GLUE: Phylogenomic Analysis of Yellow Fever Virus

<img src="md/yfv-glue-logo.png" align="right" alt="" width="280" />

YFV-GLUE is a sequence-oriented resource for comparative genomic analysis of yellow fever virus (YFV), developed using the [GLUE](https://github.com/giffordlabcvr/gluetools) software framework.

GLUE is an open, integrated software toolkit designed for storing and interpreting sequence data. It supports the creation of bespoke projects, incorporating essential data items for comparative genomic analysis, such as sequences, multiple sequence alignments, genome feature annotations, and other associated data.

Projects are loaded into the GLUE "engine," forming a relational database that represents the semantic relationships between data items. This foundation supports systematic comparative analyses and the development of sequence-based resources.

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Installation](#installation)
- [Usage](#usage)
- [Genotyping](#genotyping)
- [Mutation frequencies](#mutation-frequencies)
- [Data Sources](#data-sources)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Key Features

- **GLUE Framework Integration**: Built on the GLUE software framework, YFV-GLUE offers an extensible platform for efficient, standardized, and reproducible computational genomic analysis of yellow fever virus.

- **Phylogenetic Structure**: Sequence data in YFV-GLUE is organized in a phylogenetically-structured manner, allowing users to explore evolutionary relationships easily.

- **Rich Annotations**: Annotated reference sequences enable rigorous comparative genomic analysis related to conservation, adaptation, structural context, and genotype-to-phenotype associations.

- **Automated Genotyping**: YFV-GLUE can perform automated genotyping of YFV sequences (including subgenomic sequences) via GLUE's [maximum likelihood clade assignment (MLCA) algorithm](https://doi.org/10.1186/s12859-018-2459-9).

- **Exploratory and operational**: The GLUE framework allows sequence-based resources to be used for exploratory work in a research setting, as well as operational work in a public or animal health setting.


## Installation

If you have not done so already, install the GLUE software framework by following the [installation instructions](http://glue-tools.cvr.gla.ac.uk/#/installation) on the GLUE web site: 

Download the YFV-GLUE repository, navigate into the top-level directory, and start the GLUE command line interpreter.

At the GLUE command prompt, run the 'buildYfvProject.glue' file as follows:

```
GLUE Version 1.1.107
Copyright (C) 2015-2020 The University of Glasgow
This program comes with ABSOLUTELY NO WARRANTY. This is free software, and you
are welcome to redistribute it under certain conditions. For details see
GNU Affero General Public License v3: http://www.gnu.org/licenses/

Mode path: /
GLUE> run file buildYfvProject.glue
```

This will build (i) the base project, which contains a minimal set of feature definitions, clade categories, reference sequences, and alignments, and (ii) the extension project, which contains all YFV sequences in GenBank.

## Usage

GLUE contains an interactive command line environment focused on the development and use of GLUE projects by bioinformaticians. This provides a range of productivity-oriented features such as automatic command completion, command history and interactive paging through tabular data. 

For detailed instructions on how to use YFV-GLUE for your comparative genomic analysis, refer to the GLUE's [reference documentation](http://glue-tools.cvr.gla.ac.uk/).

## Genotyping

To classify YFV sequences via maximum likelihood clade assignment (MLCA)-based genotyping, call the appropriate genotyping module from the GLUE console, for example:

```
Mode path: /
GLUE> project yfv
OK
Mode path: /project/yfv
GLUE> module yfvMaxLikelihoodGenotyper genotype file -f path/to/sequences/YFV.fasta 
```

Please note the above command sequence is equivalent to the following:

```
Mode path: /
GLUE> project yfv module yfvMaxLikelihoodGenotyper genotype file -f path/to/sequences/YFV.fasta 
```

## Mutation frequencies

YFV-GLUE can provide a detailed frequency distribution of amino acids at a specific position within a YFV coding feature, based on the alignments contained with the project. This can enable insights into the variability and conservation of YFV proteins.

The following command in the GLUE console calculates the amino acid frequencies at a specific position within a specific feature of YFV, across an alignment of all GenBank YFV sequences:

```
Mode path: /project/yfv
GLUE> alignment AL_YFV_SouthAmerica1 amino-acid frequency -r REF_MASTER_YFV -f envelope -l 120 130
```

This command produces results in a tabular output format like this:

```
+==========+=======+===========+============+=====================+
| feature  | codon | aminoAcid | numMembers |     pctMembers      |
+==========+=======+===========+============+=====================+
| envelope | 120   | A         | 3          | 0.29673590504451036 |
| envelope | 120   | T         | 1008       | 99.70326409495549   |
| envelope | 121   | C         | 1013       | 100.0               |
| envelope | 122   | A         | 1012       | 99.90128331688055   |
| envelope | 122   | H         | 1          | 0.09871668311944719 |
| envelope | 123   | K         | 1014       | 99.80314960629921   |
| envelope | 123   | R         | 2          | 0.1968503937007874  |
| envelope | 124   | S         | 1022       | 100.0               |
| envelope | 125   | M         | 1024       | 100.0               |
| envelope | 126   | S         | 1028       | 100.0               |
| envelope | 127   | L         | 1030       | 100.0               |
| envelope | 128   | F         | 1028       | 100.0               |
| envelope | 129   | E         | 1029       | 100.0               |
| envelope | 130   | V         | 1030       | 100.0               |
+==========+=======+===========+============+=====================+
```

### Command Breakdown

**`alignment AL_YFV_SouthAmerica1`**
Selects the reference sequence-constrained alignment for the 'South America 1' genotype of YFV.

**`amino-acid frequency`**
Instructs GLUE to calculate amino acid frequencies within the selected alignment.

**`-r REF_MASTER_YFV`**
Specifies the constraining reference sequence, `REF_MASTER_YFV`, which defines the coordinate space and the wild type amino acid for comparison.

**`-f envelope`**
Indicates the coding feature within the reference sequence (envelope) where amino acid frequencies will be calculated.

**`-l 120 130`**
Specifies the location within the feature to be analyzed. Here a range is specific (120-130).

**`-a`**
Tells GLUE to use all sequence members of the alignment.

### Interpretation of the Output

- **feature**: The coding feature analyzed (in this case, envelope).
- **codon**: The codon position within the feature.
- **aminoAcid**: The amino acid found at the specified codon position.
- **numMembers**: The number of sequences in the alignment containing the specified amino acid at the given position.
- **pctMembers**: The percentage of sequences in the alignment containing the specified amino acid at the given position.


## Data Sources

YFV-GLUE relies on the following data sources:

- [NCBI Nucleotide](https://www.ncbi.nlm.nih.gov/nuccore)


## Contributing

We welcome contributions from the community! If you're interested in contributing to YFV-GLUE, please review our [Contribution Guidelines](./md/CONTRIBUTING.md).

[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](./md/code_of_conduct.md)


## License

The project is licensed under the [GNU Affero General Public License v. 3.0](https://www.gnu.org/licenses/agpl-3.0.en.html)

## Contact

For questions, issues, or feedback, please open an issue on the [GitHub repository](https://github.com/giffordlabcvr/YFV-GLUE/issues).

