# seq2mlst CHANGELOG

All noteable changes to seq2mlst will be documented in this file

## [1.0.1] 2018-04-18

### Changed
- Fixed bug in version 1.0.0: for some organisms (e.g. *Salmonella enterica*) that had different file extensions in PubMLST (i.e. not .fas), the final results files would report best-matching alleles as intended, but would not indicate in the final results file that a best-matching allele was not a perfect match (i.e. they would not append an asterisk to alleles that did not match any allele in the database with 100% identity and coverage). This is fixed in version 1.0.1.

## [1.0.0] 2017-08-07

### Added
- seq2mlst initial commit

### Changed
- On 2018-02-15, the homebrew formula was updated, as well as the README, to indicate that users should install biopython using pip, if necessary, due to issues with the homebrew formula's handling of the biopython installation
