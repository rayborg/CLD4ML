# CLD4ML: Curated Labeled Cybersecurity Datasets for Machine Learning

`CLD4ML` stands for `Curated Labeled Cybersecurity Datasets for Machine Learning`.

This README is a practical catalog of five high-value cybersecurity datasets for machine learning.

It is built to answer the questions most researchers usually have first:
- where can I get the dataset?
- how big is it?
- what is the class balance?
- what is it good for?
- what should I be careful about before I benchmark on it?

This repo includes download links for every dataset it catalogs.

Before you use those links:
- some links are official dataset pages or official download portals
- some links are mirrors that appear to host accessible copies and may be easier to use than the official source
- a mirror is not automatically official or endorsed, so always verify provenance, licensing, and citation requirements yourself

What this repo is:
- a documentation and metadata catalog
- a starting point for dataset selection and benchmark planning

What this repo is not:
- not a redistribution repo
- not a host for CSVs, ZIPs, PCAPs, TXT dumps, or other dataset payloads

How to read this page:
- use `At A Glance` if you just need a fast comparison
- use `Quick Recommendations` if you are deciding what to benchmark first
- use the dataset sections if you need counts, labels, and known issues
- use `DOWNLOAD_LINKS.md` if you want the full set of official and mirror URLs

## Contents

- [Start Here](#start-here)
- [At A Glance](#at-a-glance)
- [Quick Recommendations](#quick-recommendations)
- [Datasets](#datasets)
- [CIC-IDS-2017](#1-cic-ids-2017)
- [NSL-KDD](#2-nsl-kdd)
- [CIC-UNSW-NB15](#3-cic-unsw-nb15)
- [CSE-CIC-IDS2018](#4-cse-cic-ids2018)
- [CIC-DDoS2019](#5-cic-ddos2019)
- [Cross-Dataset Comparison Notes](#cross-dataset-comparison-notes)
- [Split Guidance](#split-guidance)
- [Label Hygiene Notes](#label-hygiene-notes)
- [Access Notes](#access-notes)
- [What This Repo Does Not Host](#what-this-repo-does-not-host)

## Start Here

- Start with `NSL-KDD` if you want the easiest classic benchmark.
- Start with `CIC-UNSW-NB15` if you want a modern flow dataset that is still manageable.
- Start with `CIC-IDS-2017` if you care about attack-family subsets and chronology-aware evaluation.
- Use `CSE-CIC-IDS2018` when you want a larger modern benchmark and can handle more cleanup.
- Use `CIC-DDoS2019` for large-scale DDoS family stress tests, not as your easiest first dataset.
- Expect cleanup work on `CSE-CIC-IDS2018` and `CIC-DDoS2019` before publication-grade experiments.

## At A Glance

Ratios are shown as `benign:attack` unless otherwise noted.

| Field | `NSL-KDD` | `CIC-UNSW-NB15` | `CIC-IDS-2017` | `CSE-CIC-IDS2018` | `CIC-DDoS2019` |
| --- | --- | --- | --- | --- | --- |
| Best for | classic reproducible IDS benchmark | modern compact flow benchmark | chronology-aware attack-family subsets | large modern day-based benchmarking | very large DDoS family stress tests |
| Measured rows | `148,517` (`train + test`) | `447,915` (`Data.csv`) | `1,788,613` in local ML snapshot | `16,233,002` | `70,427,637` |
| Benign / attack | `1.08:1` | `4.00:1` | `5.61:1` | `4.91:1` excluding malformed rows | attack-dominant (`113,828` benign vs `70,313,809` attack) |
| Columns | `43` fields (`41` features + label + difficulty) | `76` feature columns + separate label file | `79` | mostly `80`, one file `84` | `88` |
| Measured size | `26.88 MB` | `1.97 GB` | `528.04 MB` | `6.41 GB` | `3.03 GB` compressed / `28.92 GB` uncompressed |
| Access friction | low | medium | medium | low | medium |
| Key caveat | official UNB page says dataset is no longer hosted there | `Data.csv` and `Label.csv` are split; schema differs from `CICFlowMeter_out.csv` | local snapshot here excludes Monday and Friday-afternoon files | schema drift and malformed `Label` rows exist in the processed CSVs | per-file label contamination and inconsistent label naming occur |

## Quick Recommendations

- `Need a first public benchmark with minimal download pain:` `NSL-KDD`
- `Need a better modern binary benchmark than KDD-family data:` `CIC-UNSW-NB15`
- `Need day-aware or chronology-aware subset design:` `CIC-IDS-2017` or `CSE-CIC-IDS2018`
- `Need multi-family DDoS stress testing:` `CIC-DDoS2019`
- `Need the easiest publication narrative across multiple cyber datasets:` `NSL-KDD` + `CIC-UNSW-NB15` + `CIC-IDS-2017`

## Datasets

## 1. CIC-IDS-2017

**Bottom line:** best when you want semantically narrow attack-family subsets, chronology-aware splits, and modern flow-based binary benchmark construction.

### Quick Facts

| Field | Value |
| --- | --- |
| Best for | chronology-aware attack-family subsets |
| Official page | `https://www.unb.ca/cic/datasets/ids-2017.html` |
| Official portal | `https://cicresearch.ca/CICDataset/CIC-IDS-2017/` |
| Download links | `DOWNLOAD_LINKS.md#cic-ids-2017` |
| Measured rows in local snapshot | `1,788,613` |
| Benign / attack | `1,517,924 / 270,689` |
| Ratio | `5.61:1` |
| Columns | `79` |
| Measured size | `528.04 MB` |
| Best first tasks | `Bot`, `SSH-Patator`, `DoS GoldenEye` vs `BENIGN` |

### Source Links

- official dataset page: `https://www.unb.ca/cic/datasets/ids-2017.html`
- official download portal: `https://cicresearch.ca/CICDataset/CIC-IDS-2017/`
- feature extractor: `https://github.com/ISCX/CICFlowMeter`
- paper: `Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization` (Sharafaldin, Lashkari, Ghorbani, 2018)
- full access and mirror links: `DOWNLOAD_LINKS.md#cic-ids-2017`

Note:
- the CIC-IDS-2017 files summarized in this catalog were already present in a local working copy before the CLD4ML build step
- project provenance for that working copy is documented in `research/docs/dataset_description.md` in the main research workspace
- that provenance record says the local CIC-IDS-2017 CSV files were pulled from a public Hugging Face mirror because the official CICResearch download is form-gated

### Official Summary

- capture window: `2017-07-03` through `2017-07-07`
- collection duration: `5` days
- attack coverage: brute force, DoS, DDoS, Heartbleed, web attacks, infiltration, botnet, port scan
- raw day sizes from the landing page:
  - Monday `11.0 GB`
  - Tuesday `11.0 GB`
  - Wednesday `13.0 GB`
  - Thursday `7.8 GB`
  - Friday `8.3 GB`
- approximate official raw total: `51.1 GB`
- feature description: more than `80` flow features from `CICFlowMeter`

### Measured Snapshot

The metadata below was measured from source files offline during catalog construction. These files are not hosted in this repo:
- `Tuesday-WorkingHours.pcap_ISCX.csv`
- `Wednesday-workingHours.pcap_ISCX.csv`
- `Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv`
- `Thursday-WorkingHours-Afternoon-Infilteration.pcap_ISCX.csv`
- `Friday-WorkingHours-Morning.pcap_ISCX.csv`

This means:
- Monday normal-only traffic is not present in the local snapshot documented here
- Friday afternoon `PortScan` and `DDoS LOIC` are also not present in the local snapshot documented here

Snapshot totals:
- rows: `1,788,613`
- benign rows: `1,517,924`
- attack rows: `270,689`
- benign:attack ratio: `5.61:1`
- columns per file: `79`
- local ML snapshot size: `528.04 MB`

### Labels In This Snapshot

| Label | Rows |
| --- | ---: |
| `BENIGN` | `1,517,924` |
| `DoS Hulk` | `231,073` |
| `DoS GoldenEye` | `10,293` |
| `FTP-Patator` | `7,938` |
| `DoS slowloris` | `5,796` |
| `SSH-Patator` | `5,897` |
| `DoS Slowhttptest` | `5,499` |
| `Bot` | `1,966` |
| `Web Attack - Brute Force` normalized from mojibake raw label | `1,507` |
| `Web Attack - XSS` normalized from mojibake raw label | `652` |
| `Infiltration` | `36` |
| `Web Attack - Sql Injection` normalized from mojibake raw label | `21` |
| `Heartbleed` | `11` |

### Why Use It

- supports binary, multiclass, and subset-based benchmark design
- supports day-aware and chronology-aware evaluation
- strong fit for augmentation papers because single-attack subsets can be constructed cleanly
- realistic enough to remain relevant but still small enough for repeated experiments

### Typical Split

- many papers use random row-level splits
- stronger practice is day-aware or chronology-aware splitting before preprocessing
- if you are building subsets, use `BENIGN` vs one attack family at a time when possible

### Watch-Outs

- web-attack labels can appear with mojibake instead of a normal dash character
- the official dataset is broader than the local ML snapshot documented here
- the most reproducible ML workflow is to define the subset first, then split, then fit preprocessing on train only

### Good First Tasks

- `Bot vs BENIGN`
- `SSH-Patator vs BENIGN`
- `DoS GoldenEye vs BENIGN`

## 2. NSL-KDD

**Bottom line:** best classic baseline for reproducibility, light storage, and easy comparison to older IDS literature.

### Quick Facts

| Field | Value |
| --- | --- |
| Best for | classic reproducible IDS baseline |
| Official page | `https://www.unb.ca/cic/datasets/nsl.html` |
| Mirror used here | `https://github.com/defcom17/NSL_KDD` |
| Download links | `DOWNLOAD_LINKS.md#nsl-kdd` |
| Measured rows | `148,517` (`KDDTrain+` + `KDDTest+`) |
| Normal / attack | `77,054 / 71,463` |
| Ratio | `1.08:1` |
| Fields | `43` |
| Measured size | `26.88 MB` |
| Best first task | `normal vs attack` |

### Source Links

- official UNB page: `https://www.unb.ca/cic/datasets/nsl.html`
- mirror used for the curated snapshot: `https://github.com/defcom17/NSL_KDD`
- analysis paper: `https://ieeexplore.ieee.org/document/5356528`
- full access and mirror links: `DOWNLOAD_LINKS.md#nsl-kdd`

### Official Summary

- introduced to fix major redundancy problems in `KDD Cup 1999`
- standard files:
  - `KDDTrain+.TXT`
  - `KDDTrain+_20Percent.TXT`
  - `KDDTest+.TXT`
  - `KDDTest-21.TXT`
- official UNB note: the dataset is no longer directly hosted there

### Measured Snapshot

Source files measured for this catalog:
- `KDDTrain+.txt`
- `KDDTrain+_20Percent.txt`
- `KDDTest+.txt`
- `KDDTest-21.txt`

Combined main split totals (`KDDTrain+` + `KDDTest+`):
- rows: `148,517`
- normal rows: `77,054`
- attack rows: `71,463`
- benign:attack ratio: `1.08:1`
- fields per row: `43`
  - `41` features
  - `1` attack label
  - `1` difficulty field
- local snapshot size: `26.88 MB`

Detailed split counts:

| File | Rows | Normal | Attack |
| --- | ---: | ---: | ---: |
| `KDDTrain+.txt` | `125,973` | `67,343` | `58,630` |
| `KDDTest+.txt` | `22,544` | `9,711` | `12,833` |
| `KDDTest-21.txt` | `11,850` | `2,152` | `9,698` |
| `KDDTrain+_20Percent.txt` | `25,192` | `13,449` | `11,743` |

Superclass counts:

| Split | Normal | DoS | Probe | R2L | U2R |
| --- | ---: | ---: | ---: | ---: | ---: |
| `KDDTrain+` | `67,343` | `45,927` | `11,656` | `995` | `52` |
| `KDDTest+` | `9,711` | `7,458` | `2,421` | `2,887` | `67` |
| `KDDTest-21` | `2,152` | `4,342` | `2,402` | `2,887` | `67` |

### Why Use It

- tiny footprint
- fixed canonical train/test split
- still widely recognized in IDS papers
- convenient for fast baseline checks, ablations, and teaching

### Typical Split

- standard: `KDDTrain+` for train, `KDDTest+` for test
- harder generalization setting: `KDDTest-21` as test
- common practical choice: carve validation from `KDDTrain+`

### Watch-Outs

- not a modern traffic benchmark
- no realistic chronology in the way modern flow datasets provide
- good for comparability, not for strong claims of real-world realism

### Good First Tasks

- `normal vs attack`
- later, one-vs-normal family tasks for `DoS`, `Probe`, `R2L`, `U2R`

## 3. CIC-UNSW-NB15

**Bottom line:** best modern compact flow benchmark here if you want something more current than NSL-KDD without jumping straight to the scale and hygiene burden of CSE-CIC-IDS2018 or CIC-DDoS2019.

### Quick Facts

| Field | Value |
| --- | --- |
| Best for | modern compact flow benchmark |
| Official pages | `UNSW` and `UNB CIC` |
| Official portal | `https://cicresearch.ca/CICDataset/CIC-UNSW/` |
| Download links | `DOWNLOAD_LINKS.md#cic-unsw-nb15` |
| Measured rows in `Data.csv` | `447,915` |
| Benign / attack | `358,332 / 89,583` |
| Ratio | `4.00:1` |
| Columns | `76` in `Data.csv`, `84` in `CICFlowMeter_out.csv` |
| Measured size | `1.97 GB` |
| Best first tasks | `Exploits`, `DoS`, `Reconnaissance` vs `Benign` |

### Source Links

- original UNSW-NB15 page: `https://research.unsw.edu.au/projects/unsw-nb15-dataset`
- CIC-UNSW-NB15 page: `https://www.unb.ca/cic/datasets/cic-unsw-nb15.html`
- CIC download portal: `https://cicresearch.ca/CICDataset/CIC-UNSW/`
- original UNSW-NB15 paper: `https://ieeexplore.ieee.org/abstract/document/7348942`
- CIC-UNSW-NB15 augmentation paper: `Poisoning and Evasion: Deep Learning-Based NIDS under Adversarial Attacks` (Mohammadian, Lashkari, Ghorbani, 2024)
- full access links: `DOWNLOAD_LINKS.md#cic-unsw-nb15`

### Official Summary

- original raw capture size: about `100 GB`
- original record count: `2,540,044`
- attack categories: `9`
  - `Fuzzers`
  - `Analysis`
  - `Backdoor`
  - `DoS`
  - `Exploits`
  - `Generic`
  - `Reconnaissance`
  - `Shellcode`
  - `Worms`
- original standard split files:
  - `UNSW_NB15_training-set.csv` with `175,341` rows
  - `UNSW_NB15_testing-set.csv` with `82,332` rows

### Measured Snapshot

Source files measured for this catalog:
- `CICFlowMeter_out.csv`
- `Data.csv`
- `Label.csv`
- `Readme.txt`

`Data.csv` snapshot:
- rows: `447,915`
- feature columns: `76`
- labels stored separately in `Label.csv`
- benign rows: `358,332`
- attack rows: `89,583`
- benign:attack ratio: `4.00:1`

`CICFlowMeter_out.csv` snapshot:
- rows: `3,540,241`
- columns: `84` including `Label`
- benign rows: `3,450,658`
- attack rows: `89,583`

Local snapshot size:
- total local size: `1.97 GB`

### Labels In This Snapshot (`Data.csv` / `Label.csv`)

| Label | Rows |
| --- | ---: |
| `Benign` | `358,332` |
| `Exploits` | `30,951` |
| `Fuzzers` | `29,613` |
| `Reconnaissance` | `16,735` |
| `Generic` | `4,632` |
| `DoS` | `4,467` |
| `Shellcode` | `2,102` |
| `Backdoor` | `452` |
| `Analysis` | `385` |
| `Worms` | `246` |

### Why Use It

- much more modern than KDD-family benchmarks
- easier to handle than CSE-CIC-IDS2018 at full scale
- clean attack-family inventory for one-vs-benign subset design
- good fit for binary family-level tasks such as `Exploits vs Benign`

### Typical Split

- original UNSW papers often use the provided train/test files
- CIC-UNSW users often work directly from `Data.csv` and `Label.csv`
- if chronology is not trustworthy in the derived file, use one deterministic stratified train/val/test split

### Watch-Outs

- `Data.csv` has no inline label column; labels live in `Label.csv`
- `CICFlowMeter_out.csv` and `Data.csv` do not share the same schema width
- if you compare against original UNSW-NB15 papers, be explicit about whether you are using original UNSW files or the CIC-UNSW augmented flow extraction

### Good First Tasks

- `Exploits vs Benign`
- `DoS vs Benign`
- `Reconnaissance vs Benign`

## 4. CSE-CIC-IDS2018

**Bottom line:** strongest choice here when you want a large, modern, multi-day cyber benchmark and are willing to do more dataset hygiene work.

### Quick Facts

| Field | Value |
| --- | --- |
| Best for | large modern day-based benchmarking |
| Official page | `https://www.unb.ca/cic/datasets/ids-2018.html` |
| AWS registry | `https://registry.opendata.aws/cse-cic-ids2018/` |
| Download links | `DOWNLOAD_LINKS.md#cse-cic-ids2018` |
| Measured rows | `16,233,002` |
| Benign / attack | `13,484,708 / 2,748,235` plus `59` malformed rows |
| Ratio | `4.91:1` excluding malformed rows |
| Columns | mostly `80`, one file `84` |
| Measured size | `6.41 GB` |
| Best first tasks | `Bot`, `Brute Force`, `DoS/DDoS` vs `Benign` |

### Source Links

- official UNB page: `https://www.unb.ca/cic/datasets/ids-2018.html`
- AWS registry page: `https://registry.opendata.aws/cse-cic-ids2018/`
- public bucket: `s3://cse-cic-ids2018/`
- public listing endpoint: `https://cse-cic-ids2018.s3.ca-central-1.amazonaws.com?list-type=2`
- paper link on AWS page: `http://www.scitepress.org/Papers/2018/66398/66398.pdf`
- full access and direct CSV links: `DOWNLOAD_LINKS.md#cse-cic-ids2018`

### Official Summary

- collaborative project between `CSE` and `CIC`
- attack scenarios: `7`
  - brute force
  - heartbleed
  - botnet
  - DoS
  - DDoS
  - web attacks
  - infiltration
- environment scale:
  - `50` attacker machines
  - `420` victim PCs
  - `30` victim servers
- feature extraction: more than `80` features from `CICFlowMeter-V3`

### Measured Snapshot

Processed ML CSV files measured for this catalog:
- `Friday-02-03-2018_TrafficForML_CICFlowMeter.csv`
- `Friday-16-02-2018_TrafficForML_CICFlowMeter.csv`
- `Friday-23-02-2018_TrafficForML_CICFlowMeter.csv`
- `Thuesday-20-02-2018_TrafficForML_CICFlowMeter.csv`
- `Thursday-01-03-2018_TrafficForML_CICFlowMeter.csv`
- `Thursday-15-02-2018_TrafficForML_CICFlowMeter.csv`
- `Thursday-22-02-2018_TrafficForML_CICFlowMeter.csv`
- `Wednesday-14-02-2018_TrafficForML_CICFlowMeter.csv`
- `Wednesday-21-02-2018_TrafficForML_CICFlowMeter.csv`
- `Wednesday-28-02-2018_TrafficForML_CICFlowMeter.csv`

Processed snapshot totals:
- rows: `16,233,002`
- benign rows: `13,484,708`
- attack rows: `2,748,235`
- malformed literal `Label` rows: `59`
- benign:attack ratio excluding malformed rows: `4.91:1`
- columns:
  - most files: `80`
  - `Thuesday-20-02-2018_TrafficForML_CICFlowMeter.csv`: `84`
- processed ML CSV snapshot size: `6.41 GB`

### Labels In This Snapshot

| Label | Rows |
| --- | ---: |
| `Benign` | `13,484,708` |
| `DDOS attack-HOIC` | `686,012` |
| `DDoS attacks-LOIC-HTTP` | `576,191` |
| `DoS attacks-Hulk` | `461,912` |
| `Bot` | `286,191` |
| `FTP-BruteForce` | `193,360` |
| `SSH-Bruteforce` | `187,589` |
| `Infilteration` | `161,934` |
| `DoS attacks-SlowHTTPTest` | `139,890` |
| `DoS attacks-GoldenEye` | `41,508` |
| `DoS attacks-Slowloris` | `10,990` |
| `DDOS attack-LOIC-UDP` | `1,730` |
| `Brute Force -Web` | `611` |
| `Brute Force -XSS` | `230` |
| `SQL Injection` | `87` |
| malformed literal `Label` rows | `59` |

### Why Use It

- broad modern attack coverage
- much larger scale than CIC-IDS-2017
- useful for day-based generalization, held-out-day testing, and attack-window evaluation
- strong candidate for cross-dataset validation once a method is stable on smaller benchmarks

### Typical Split

- many papers use day-based or file-based splits
- weaker practice is global random row shuffling
- stronger practice is day-aware, attack-window-aware, or held-out-day evaluation

### Watch-Outs

- there is schema drift: one file has `84` columns while most have `80`
- some files contain malformed rows where the label value is literally `Label`
- `Infilteration` is misspelled in the dataset and should usually be preserved verbatim in raw parsing code, then normalized downstream

### Good First Tasks

- `Bot vs Benign`
- `Brute Force vs Benign`
- `DoS or DDoS family vs Benign`

## 5. CIC-DDoS2019

**Bottom line:** best when you need a large family-level DDoS benchmark, but it needs the most hygiene before it becomes a clean ML paper benchmark.

### Quick Facts

| Field | Value |
| --- | --- |
| Best for | large-scale DDoS family stress tests |
| Official page | `https://www.unb.ca/cic/datasets/ddos-2019.html` |
| Official portal | `https://cicresearch.ca/CICDataset/CICDDoS2019/` |
| Download links | `DOWNLOAD_LINKS.md#cic-ddos2019` |
| Measured rows | `70,427,637` |
| Benign / attack | `113,828 / 70,313,809` |
| Composition | strongly attack-dominant |
| Columns | `88` |
| Measured size | `3.03 GB` compressed / `28.92 GB` uncompressed |
| Best first tasks | `Syn`, `UDP`, `LDAP or DNS` vs `Benign` |

### Source Links

- official dataset page: `https://www.unb.ca/cic/datasets/ddos-2019.html`
- official download portal: `https://cicresearch.ca/CICDataset/CICDDoS2019/`
- cited paper: `https://ieeexplore.ieee.org/abstract/document/8888419`
- full access links: `DOWNLOAD_LINKS.md#cic-ddos2019`

### Official Summary

- focus: reflective and exploitation-based DDoS attack taxonomy
- organization: first day and second day
- attack families named on the landing page:
  - `PortMap`
  - `NetBIOS`
  - `LDAP`
  - `MSSQL`
  - `UDP`
  - `UDP-Lag`
  - `SYN`
  - `NTP`
  - `DNS`
  - `SNMP`
  - `SSDP`
  - `WebDDoS`
  - `TFTP`
- feature extraction: more than `80` traffic features via `CICFlowMeter-V3`

### Measured Snapshot

Archives measured for this catalog:
- `CSV-01-12.zip`
- `CSV-03-11.zip`

Archive snapshot totals:
- rows: `70,427,637`
- benign rows: `113,828`
- attack rows: `70,313,809`
- overall composition: strongly attack-dominant
- columns: `88`
- compressed local size: `3.03 GB`
- uncompressed CSV size: `28.92 GB`

### Labels In This Snapshot

| Label | Rows |
| --- | ---: |
| `TFTP` | `20,082,580` |
| `Syn` | `6,473,789` |
| `MSSQL` | `5,787,453` |
| `DrDoS_SNMP` | `5,159,870` |
| `DrDoS_DNS` | `5,071,011` |
| `DrDoS_MSSQL` | `4,522,492` |
| `DrDoS_NetBIOS` | `4,093,279` |
| `UDP` | `3,867,155` |
| `NetBIOS` | `3,657,497` |
| `DrDoS_UDP` | `3,134,645` |
| `DrDoS_SSDP` | `2,610,611` |
| `DrDoS_LDAP` | `2,179,930` |
| `LDAP` | `1,915,122` |
| `DrDoS_NTP` | `1,202,642` |
| `UDP-lag` | `366,461` |
| `Portmap` | `186,960` |
| `UDPLag` | `1,873` |
| `WebDDoS` | `439` |
| `BENIGN` | `113,828` |

### Why Use It

- extreme-scale DDoS family benchmarking
- very useful for family-level detection and one-family-vs-benign tasks
- a strong stress test for augmentation methods on high-volume attack data

### Typical Split

- many papers use first-day vs second-day separation
- others collapse everything into a binary `BENIGN vs DDoS` task
- stronger practice is to keep family-level tasks separate and preserve day structure where possible

### Watch-Outs

- some files named after one family contain rows from other labels
- label naming is inconsistent, for example `UDP-lag` vs `UDPLag`
- the dataset is not naturally benign-majority overall in the downloaded CSV bundle; naive `attack vs benign` experiments can therefore be misleading
- this dataset is best treated as a set of family-specific benchmark sources, not as one monolithic binary table

### Good First Tasks

- `Syn vs Benign`
- `UDP vs Benign`
- `LDAP vs Benign` or `DNS vs Benign`

## Cross-Dataset Comparison Notes

### Best First Public Benchmark Stack

If you want a practical three-dataset stack for a paper:
- `NSL-KDD` for classic comparability
- `CIC-UNSW-NB15` for modern compact flow benchmarking
- `CIC-IDS-2017` for chronology-aware attack-family subsets

### Strongest Four-Dataset Stack

If you want a stronger generalization story:
- `NSL-KDD`
- `CIC-UNSW-NB15`
- `CIC-IDS-2017`
- `CSE-CIC-IDS2018`

### When To Add `CIC-DDoS2019`

Add `CIC-DDoS2019` when:
- your pipeline is already stable on cleaner datasets
- you want DDoS-family-specific stress tests
- you are willing to normalize labels and isolate cleaner family-level subsets first

## Split Guidance

Recommended split policy by dataset:

- `CIC-IDS-2017`
  - prefer chronology-aware or day-aware split before preprocessing
- `NSL-KDD`
  - use `KDDTrain+` / `KDDTest+`, with validation carved from train
- `CIC-UNSW-NB15`
  - use one deterministic stratified split if you are not using the original UNSW train/test files
- `CSE-CIC-IDS2018`
  - use day-aware or attack-window-aware splits, not naive global shuffling
- `CIC-DDoS2019`
  - preserve day separation and isolate one DDoS family per benchmark when possible

## Label Hygiene Notes

- `CIC-IDS-2017`: web-attack labels may contain mojibake in some mirrors
- `CSE-CIC-IDS2018`: malformed `Label` rows exist and should be filtered
- `CSE-CIC-IDS2018`: `Infilteration` is misspelled in the source data
- `CIC-DDoS2019`: inconsistent label naming and cross-file label contamination occur
- `CIC-UNSW-NB15`: `Data.csv` requires `Label.csv` to recover class labels
- `NSL-KDD`: use exact official filenames and keep the difficulty field if you want full compatibility with older work

## Access Notes

- `NSL-KDD` official UNB landing page exists, but the dataset is no longer directly downloadable there; a mirror is needed.
- `CIC-IDS-2017`, `CIC-UNSW-NB15`, and `CIC-DDoS2019` use web-form-gated download portals.
- `CSE-CIC-IDS2018` is the easiest to automate because the AWS bucket is public.

## What This Repo Does Not Host

- no raw dataset files
- no processed dataset files
- no mirrored ZIP archives
- no PCAPs, CSVs, TXT dumps, or label files from the source datasets
- only documentation, URLs, and measured metadata summaries

## Citation And License Reminder

Do not assume these datasets are public-domain.

For each dataset:
- read the official page
- cite the primary paper named by the data owner
- preserve any redistribution restrictions or citation requirements

## Why These Five

These five were chosen because together they cover:
- classic vs modern IDS benchmarking
- small vs very large scale
- balanced-ish vs severely imbalanced regimes
- general intrusion detection vs specialized DDoS evaluation
- fixed splits, day-aware splits, and chronology-aware subset design

That makes them a strong core catalog for public ML benchmarking work in cybersecurity.
