BioScope Scientific Uncertainty Classification (derived CSV dataset)
===================================================================
Original dataset: BioScope corpus (Vincze et al., BMC Bioinformatics 2008)
Official corpus page: https://rgai.inf.u-szeged.hu/node/105
Original archive used: bioscope.zip, supplied by the user

SOURCE FILES:
- abstracts.xml: included only AbstractText sentences; excluded document titles.
- full_papers.xml: included only Text sentences; excluded section headings,
  figure/table legends, and document titles.
- The clinical records were EXCLUDED due to clinical-text licensing and
  because the project concerns scientific statements.

LABELS:
- 1 / uncertain: original sentence contains at least one
  <cue type="speculation"> annotation at any depth.
- 0 / non_uncertain: no original speculation cue.
- Negation-only sentences remain label 0 (not uncertainty).
- IMPORTANT: BioScope encodes speculative linguistic cues/hedges; this is
  NOT a measured 1-to-6 degree of certainty. It is not interchangeable with
  all certainty dimensions in the Pei & Jurgens dataset.

SPLITTING / CLEANING:
- Train / dev / test split with seed=42, and document-level grouping.
- 80/10/10 approximate by number of original documents; full papers: 7/1/1.
- Collapsed whitespace, removed rare identical duplicate sentences globally
  (train > dev > test priority), preserving gold labels.
- Kept original annotated sentences otherwise, including biological names.

COLUMNS:
text: sentence with inline XML tags flattened away
label: 0 or 1
label_name: non_uncertain or uncertain
document_id: unique source document identifier (used for leak-free splitting)
sentence_id: source XML sentence id
source: abstract or full_article

SPLIT COUNTS:
- train: 10175 sentences = 8143 non_uncertain + 2032 uncertain; 1025 documents.
- dev: 1291 sentences = 1022 non_uncertain + 269 uncertain; 128 documents.
- test: 1491 sentences = 1196 non_uncertain + 295 uncertain; 129 documents.
- Total: 12957 labeled sentences.
- Removed duplicate sentence records: {'train': 24, 'dev': 2, 'test': 0}; total=26.

RESEARCH CAUTIONS:
- Domain: biomedical papers, not physics.
- Labels indicate *presence of a speculation cue*, not factual truth.
- Do not split sentences randomly again; preserve original document groups.
- Report macro-F1, positive-class F1, precision, recall, and support;
  classes are imbalanced.
- Manual audit of illustrative examples is recommended.

CITATION:
Vincze, V., Szarvas, G., Farkas, R., Mora, G., & Csirik, J. (2008).
The BioScope corpus: biomedical texts annotated for uncertainty, negation
and their scopes. BMC Bioinformatics 9(Suppl 11):S9.
https://doi.org/10.1186/1471-2105-9-S11-S9
