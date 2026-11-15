# Data

The notebook reads two files from this directory. Neither is committed — they are public but large, and
they are better downloaded from source than duplicated here.

## Source

Both files come from the **MSK-IMPACT 2017** study on cBioPortal:

- Study page: <https://www.cbioportal.org/study/summary?id=msk_impact_2017>
- Bulk download: <https://github.com/cBioPortal/datahub/tree/master/public/msk_impact_2017>

Citation: Zehir A, et al. *Mutational landscape of metastatic cancer revealed from prospective clinical
sequencing of 10,000 patients.* Nature Medicine, 2017. cBioPortal itself is described in Cerami et al.
(2012) and Gao et al. (2013).

## Files expected

| Filename | What it is | Shape in the original run |
| --- | --- | --- |
| `msk_impact_2017_clinical_data.tsv` | Tab-separated clinical table, one row per sample | 78,264 rows × 27 columns |
| `data_mutations.txt` | Mutation calls in MAF format, one row per variant | see source |

Column names the notebook depends on: `Sample ID`, `Primary Tumor Site`, `Metastatic Site`,
`Sample Type`, `Mutation Count`, `Smoking History`. The MAF cells use `Hugo_Symbol` and
`Tumor_Sample_Barcode`.

The MAF starts with a `#sequenced_samples:` comment line, which is why the notebook reads it with
`comment='#'`. If you use a different cBioPortal export and get a `ParserError`, check for that line
first.

## Getting them

Use the **Download** tab on the cBioPortal study page:

1. *Clinical Data* → gives `msk_impact_2017_clinical_data.tsv`, already merged across patient and sample
   attributes with the human-readable column names the notebook expects.
2. *Mutations* → gives the MAF. Rename it to `data_mutations.txt` if the download is called something
   else.

Then move both into this `data/` directory.

The datahub repository is the other route, but its files are split differently: clinical attributes sit
in `data_clinical_patient.txt` and `data_clinical_sample.txt`, with uppercase column names
(`PRIMARY_SITE`, `METASTATIC_SITE`, …) and no `Mutation Count` or `Smoking History` in the sample file.
If you use it you will need to join the two tables and rename the columns before the notebook will run,
so the web export is the path of least resistance. The datahub files are also stored with Git LFS, so a
plain `curl` against `raw.githubusercontent.com` returns a pointer file rather than the data.

## Terms

The data is de-identified and released for research use through cBioPortal under its own terms. It is
not redistributed in this repository, and nothing here overrides those terms.
