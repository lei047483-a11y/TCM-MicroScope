# Dataset Card for TCM-MicroScope

## Summary

TCM-MicroScope is a four-domain dataset for cross-domain classification of microscopic images of traditional Chinese medicinal materials. It contains 4,679 images from 12 classes. The four domains differ in imaging devices, scan parameters, and sample origins.

## Intended uses

The dataset is intended for research on cross-domain microscopic image classification, domain adaptation, domain generalization, robustness to acquisition-device changes, and fine-grained recognition of traditional Chinese medicinal materials.

The dataset is not intended to replace expert identification, clinical judgment, pharmacopoeial examination, or regulatory quality control.

## Composition and roles

| Domain | Images | Experimental use |
|---|---:|---|
| D1 | 2,902 | Labeled source-domain training data |
| D2_train | 554 | Labeled seen-target training data |
| D2_val | 254 | Hyperparameter selection, model selection, and seen-target validation |
| D3 | 802 | Held-out unseen-domain testing |
| D4 | 167 | Held-out unseen-domain testing |

Class-level counts and folder-name mappings are available in [`CLASS_MAPPING.csv`](CLASS_MAPPING.csv).

## Data organization

Labels are represented by directory names. The public directory structure preserves the experimental split. D2_val, D3, and D4 should not be merged into the training data when comparing against the paper.

## Collection and split scope

D1 contains optical-microscope images. D2 was collected using a digital scanner. D3 and D4 come from device models and vendors not encountered during training. The shifts among domains arise from differences in imaging devices, scan parameters, and sample origins.

D2_train and D2_val are image/field-of-view-level splits. Specimen-level, slide-level, or acquisition-session independence between them is not claimed.

## Evaluation protocol

1. Train using labeled D1 and D2_train data.
2. Use D2_val for hyperparameter selection, model selection, and seen-target validation.
3. Keep D3 and D4 unavailable during training, prototype construction, hyperparameter tuning, and model selection.
4. Evaluate the fixed model on D3 and D4 as unseen target domains.

Using D3 or D4 to tune a model produces a different protocol and should be reported explicitly.

## Known limitations

- The dataset contains 12 classes and does not cover the full diversity of traditional Chinese medicinal materials.
- Class frequencies differ across domains.
- Device, sample-source, and acquisition differences may be partially confounded.
- D2_train and D2_val are not claimed to be specimen-independent.
- Exact-hash checking does not detect every near duplicate, overlapping field of view, or repeated specimen.
- Performance on this dataset does not establish reliability in clinical, regulatory, or routine production settings.

## Versioning

The initial public release should be tagged as `v1.0.0` only after the image counts, duplicate audit, license, and repository links have been finalized. Later file replacements, label corrections, or split changes should receive a new version and be recorded in a changelog.

## Citation

Please cite the associated TAPM-Net paper. Bibliographic details will be added after publication.

## Corrections

Please use GitHub Issues to report suspected duplicates, label errors, corrupted images, or documentation problems. Include the relative file path and a concise description.
