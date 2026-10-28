# TCM-MicroScope

TCM-MicroScope is a four-domain microscopic image dataset for cross-domain classification of traditional Chinese medicinal materials. It contains 12 classes acquired under different imaging conditions. The release accompanies the manuscript:

> **TAPM-Net: A Target-Aware Prototype Rectification and Memory Learning Network for Cross-Domain TCM Microscopic Image Classification**

Repository: <https://github.com/lei047483-a11y/TCM-MicroScope>

## Dataset organization

```text
TCM-MicroScope/
|-- dataset1/                  # D1: labeled source domain
|-- dataset2mo/
|   |-- train/                 # D2_train: seen-target training split
|   `-- val/                   # D2_val: seen-target validation split
|-- dataset3/                  # D3: unseen target domain
`-- dataset4/                  # D4: unseen target domain
```

Each domain or split contains one folder per class. Folder and image names use lowercase English identifiers with underscores, as listed in [`CLASS_MAPPING.csv`](CLASS_MAPPING.csv).

## Image counts

| Domain or split | Role | Images |
|---|---|---:|
| `dataset1` | D1 labeled source domain | 2,902 |
| `dataset2mo/train` | D2_train labeled seen-target training split | 554 |
| `dataset2mo/val` | D2_val seen-target validation split | 254 |
| `dataset3` | D3 unseen target test domain | 802 |
| `dataset4` | D4 unseen target test domain | 167 |
| **Total** |  | **4,679** |

Class-level counts are provided in [`CLASS_MAPPING.csv`](CLASS_MAPPING.csv).

## Experimental protocol

- D1 and D2_train are the only domains used for model training and prototype construction.
- D2_val is used for hyperparameter selection, model selection, and validation on the seen target domain.
- D3 and D4 are held-out unseen target domains. They are not used for training, prototype construction, hyperparameter tuning, or model selection.
- Results on D3 and D4 should be obtained only after all choices have been fixed using D1, D2_train, and D2_val.

This protocol should be preserved when comparing with the results reported in the manuscript.

## Domain definition and split scope

D1 contains optical-microscope images and serves as the labeled source domain. D2 was collected using a digital scanner and serves as the seen target domain. It is divided into D2_train and D2_val. D3 and D4 come from device models and vendors not encountered during training and serve as unseen target domains.

D2_train and D2_val are image/field-of-view-level splits. Specimen-level, slide-level, or acquisition-session independence between them is not claimed.

## Classes

The dataset contains the following 12 classes:

1. Arborvitae seed (`arborvitae_seed`)
2. Processed pinellia (`processed_pinellia`)
3. Szechuan lovage rhizome (`szechuan_lovage_rhizome`)
4. Vinegar-processed schisandra (`vinegar_processed_schisandra`)
5. Chinese angelica (`chinese_angelica`)
6. Codonopsis root (`codonopsis_root`)
7. Poria (`poria`)
8. Cinnamon bark (`cinnamon_bark`)
9. Sour jujube seed (`sour_jujube_seed`)
10. Honey-fried licorice (`honey_fried_licorice`)
11. Honey-fried astragalus (`honey_fried_astragalus`)
12. Cinnabar (`cinnabar`)

## Preprocessing used in the paper

In the reported experiments, images were converted to RGB, padded with white pixels to a square canvas, resized to 512 x 512 pixels, and normalized using ImageNet statistics. The feature pipeline used the original RGB, grayscale-to-RGB, and horizontal-flip views with scale factors of 0.95, 1.00, and 1.05. No color jitter, random rotation, MixUp, or CutMix was applied.

## Integrity and leakage control

Exact-file duplicate checking is performed using SHA-256 hashes. Duplicates within D1 are retained because D1 was supplied as an expert-provided source set. The release is checked for:

- exact duplicates within D2_train, D2_val, D3, and D4;
- exact duplicates across D2_train, D2_val, D3, and D4; and
- exact overlap between D1 and D2-D4.

This check concerns exact file content. It does not establish specimen-level independence or detect every possible near duplicate or overlapping field of view.

## Citation

If you use this dataset, please cite the associated TAPM-Net paper. Full bibliographic information will be added after publication.

```text
TAPM-Net: A Target-Aware Prototype Rectification and Memory Learning Network
for Cross-Domain TCM Microscopic Image Classification.
```

## License

The dataset owner must select and add the final license before public release. Until a license file is added, the presence of files in this repository should not be interpreted as granting reuse rights. See [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md).

## Contact

Questions and correction reports may be submitted through the repository's GitHub Issues page.
