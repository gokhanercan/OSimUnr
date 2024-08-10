# OSimUnr: Orthographically Similar but Semantically Unrelated Word-pairs Dataset

The OSimUnr dataset consists of nearly one million noun word-pairs (wps) for the English and Turkish languages. Final relatedness scores of such word-pairs are obtained through graph-based WordNet similarity/relatedness approximation methods, which are known to be roughly 50% correlated with human annotated relatedness scores. The dataset does not contain any human-annotated data. Word-pairs are automatically selected by a complex pipeline, designed for a specific scenario: *orthographically-similar-but-semantically-unrelated (OSimUnr)*. Some cherry-picked examples are:


| English                  | Turkish                   |
| :------------------------- | --------------------------- |
| processor - professor    | tencere - pencere         |
| adventure - denture      | tesbih - teşbih          |
| souffle - shuffle        | kiracılık - biracılık |
| fridge - fringe          | enişte - erişte         |
| internet - intercept     | kampanya - şampanya      |
| lockdown - lookdown      | avanta - lavanta          |
| undergrad - underground  | piyangocu - piyanocu      |
| margin - margarin        | bakara - makara           |
| shrine - shrink          | istifa - istifra          |
| dictionary - reactionary | kıyafet - kıyamet       |

## Final Data Files (Quick download)

Below are the download links for the final data files:

| osim alg. | English (#)                                                   | Turkish                                                       |
| ----------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| editsim   | [OSimUnr-editsim-EN](OSimUnr-editsim-EN.rar) (570,172 wps)    | [OSimUnr-editsim-TR](OSimUnr-editsim-TR.rar) (333,963 wps)    |
| over_ft23 | [OSimUnr-over_ft23-EN](OSimUnr-over_ft23-EN.csv) (69,821 wps) | [OSimUnr-over_ft23-TR](OSimUnr-over_ft23-TR.csv) (38,057 wps) |

See 'All Resources' section, if you have read the paper and need more specific outputs from individual pipeline stages or final data files which are grouped by Q3-Q4 definitions and two orthographic similarity algorithms.

## All Resources

Following table lists artifacts generated from each stage of the study OSimUnr. Please [see the paper](#) for further details.

### Stage 1: Word-pool Selection

Single noun words only. Multi-word phrases (e.g., *business suit*, *change of color*) and words with punctuations (e.g., *a-team*, *9/11*, *500*) are filtered out. All words and word-pairs are given in lowercase. Proper nouns (e.g., *einstein*) are included.

| Stage | Type | English                                                           | Turkish                                                           |
| ------- | ------ | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| 1     | word | [S1-FinalWordPool-EN.txt](S1-FinalWordPool-EN.txt) (46,434 words) | [S1-FinalWordPool-TR.txt](S1-FinalWordPool-TR.txt) (24,952 words) |

<!--
| 1     | word (in)  | [S1-SingleWordPool-EN.txt](S1-SingleWordPool-EN.txt) (83,118 words) | S1-SingleWordPool-TR.txt         |
-->

### Stage 2 and 3: Word Pairing and Relatedness Filtering

Stage 2 exhaustively pairs all words in the word pool (from Stage 1) and keeps word-pairs that are **orthographically similar**. The orthographic similarity of these pairs are calculated using *editsim* and *over_ft23* algorithms.

Stage 3 eliminates semantically related (e.g., relatedness) word-pairs using a separate pipeline, which utilizes many morphological and semantic resources.

| #         | Stage                        | Type | English  - editsim (#)                              | English - over_ft23 (#)                               | Turkish -editsim (#)                               | Turkish - over_ft23 (#)                               |
| ----------- | ------------------------------ | ------ | :---------------------------------------------------- | ------------------------------------------------------- | :--------------------------------------------------- | :------------------------------------------------------ |
| 2         | Orthographically Similars (OSim)    | wp   | [Q3](S2-OrthographicallySimilarsQ3-editsim-EN.rar) (~4.6M) | [Q3](S2-OrthographicallySimilarsQ3-over_ft23-EN.rar) (~1.1M) | [Q3](S2-OrthographicallySimilarsQ3-editsim-TR.rar) (~2M)  | [Q3](S2-OrthographicallySimilarsQ3-over_ft23-TR.csv) (~406K) |
|           |                              | wp   | [Q4](S2-OrthographicallySimilarsQ4-editsim-EN.csv) (~54K)  | [Q4](S2-OrthographicallySimilarsQ4-over_ft23-EN.csv) (~37K)  | [Q4](S2-OrthographicallySimilarsQ4-editsim-TR.csv) (~31K) | [Q4](S2-OrthographicallySimilarsQ4-over_ft23-TR.csv) (~18K)  |
| 3         | Relatedness Filtering        | wp   | [Q3](S3-OSimUnrQ3-editsim-EN.rar) (~567K)           | [Q3](S3-OSimUnrQ3-over_ft23-EN.csv) (~68K)            | [Q3](S3-OSimUnrQ3-editsim-TR.csv) (~332K)          | [Q4](S3-OSimUnrQ3-over_ft23-TR.csv) (~38K)            |
|           |                              | wp   | [Q4](S3-OSimUnrQ4-editsim-EN.csv) (2,715)           | [Q4](S3-OSimUnrQ4-over_ft23-EN.csv) (1,149)           | [Q4](S3-OSimUnrQ4-editsim-TR.csv) (1,844)          | [Q4](S3-OSimUnrQ4-over_ft23-TR.csv) (539)             |
| **Final** | **OSimUnr** (Q3+Q4 combined) | wp   | [OSimUnr-editsim ](OSimUnr-editsim-EN.rar)(~570K)   | [OSimUnr-over_ft23](OSimUnr-over_ft23-EN.csv) (~70K)  | [OSimUnr-editsim](OSimUnr-editsim-TR.rar)(~334K)   | [OSimUnr-over_ft23](OSimUnr-over_ft23-TR.csv)(~38)    |

## Methodology and Notes

* All word-pairs are automatically generated by complex NLP pipelines (selection, pairing, filtering, scoring) relying on many **morphological resources** for Turkish and English languages.
* All orthographic similarity and semantic relatedness scores are normalized (0,1).

## Definitions and Abbreviations

**wp(s):** word-pair(s)

**w1:** First word of word-pair.

**w2:** Second word of word-pair.

**osim:** Orthographic similarity (i.e., string similarity) score of words calculated by two separate algorithms (editsim or over_ft23).

**editsim:** Orthographic similarity score calculated with inverted version of normalized edit distance. Formula: *1 - normalized(editdistance(w1, w2))*. Higher numbers denote higher orthographic similarity.

**over_ft23:** Normalized orthographic similarity metric calculates the overlapping factor of possible n-grams of words in a word-pair. It is proposed in the paper.

**Q3:** Word-pairs where osim scores are between 0.5 and 0.75.

**Q4:** Word-pairs where osim scores are between 0.75 and 1.

**Q3 + Q4:** Word-pairs where osim scores are between 0.5 and 1.

**orthographically similar (OSIM):** A word-pair is *orthographically similar* if the osim score is greater than or equal to 0.50.

**semantically unrelated (UNR):** A word-pair is defined *unrelated* if the relatedness score of the word-pair is less than or equal to 0.25.

**wn_lch:** WordNet-based lch (Claudia Leacock and Martin Chodorow) semantic similarity/relatedness score.

**wn_wup:** WordNet-based wup (Zhibiao Wu and Martha Palmer) semantic similarity/relatedness score.

<!---
## Cite

If you use these resources on your research, please cite the following paper:

Grammar or Crammer? The Role of Morphology on Distinguishing Orthographically Similar but Semantically Unrelated Words
[(Details)](http://www.gokhanercan.com/publications.aspx?paper=osimunr)

```bib
@inproceedings{arxiv-id,
Grammar or Crammer? The Role of Morphology on Distinguishing Orthographically Similar but Semantically Unrelated Words
}
```
-->