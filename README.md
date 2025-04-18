# NVS-SQA

Official implementation of "NVS-SQA: Exploring Self-Supervised Quality Representation Learning for Neurally Synthesized Scenes without References" [arxiv](https://arxiv.org/abs/2501.06488)).


### Generating No-Reference Quality Representations with the Pretrained Model

#### Installation

You can install the package directly from PyPI:

```bash
pip install nvs_sqa
```

#### Usage

The package can be used programmatically. You can download the **examples folder** [here](https://github.com/VincentQQu/NVS-SQA/tree/main/examples). Here's an example of how to generate quality features and scores:

```python
import nvs_sqa

# Initialize the QualityAssessor
qa = nvs_sqa.QualityAssessor()

# Define the evaluation folder path containing NSS directories
eval_folder = "./examples"

# Generate quality features
all_feats, save_path = qa.generate_quality_features(eval_folder, verbose=True)

# Compute quality scores
quality_scores = qa.generate_quality_scores(all_feats, verbose=True)

print(f"Features saved to: {save_path}")
```

#### About the Output

1. **Feature Generation and Saving**: The `generate_quality_features` method processes each NSS folder in the evaluation directory, generates quality features for each, and saves these features in a `.npz` file. The output is in the format of `{<nss_name>: 384-dim rep., ...}`. You can use `np.load()` to load it.

2. **Quality Scores**: The `generate_quality_scores` method calculates quality scores based on the generated features by applying a ridge linear regression model trained on the Fieldwork, Lab, and LLFF datasets.

3. **Example NSS**: You can find example NSS data in the repository's `examples` folder, which includes scenes generated by GNT-Cross-scene and Plenoxel.

#### Important Notes:

- **JOD Scoring Format**: The JOD score, which is the adopted scoring format, features primarily negative values (offset by reference quality), with higher scores indicating better quality.
- **Relevance of JOD Scores**: According to the dataset authors for Fieldwork and Lab, JOD scores are more meaningful within the same scene, suggesting that cross-scene comparisons of JOD scores may not provide meaningful insights.




### To Cite
<pre>

@article{qu2025nvs,
  title={NVS-SQA: Exploring Self-Supervised Quality Representation Learning for Neurally Synthesized Scenes without References},
  author={Qu, Qiang and Shen, Yiran and Chung, Yuk Ying and Cai, Weidong and Chen, Xiaoming and Liu, Tongliang},
  journal={arXiv preprint arXiv:2501.06488},
  year={2025}
}

@article{qu2024nerf,
  title={NeRF-NQA: No-Reference Quality Assessment for Scenes Generated by NeRF and Neural View Synthesis Methods},
  author={Qu, Qiang and Liang, Hanxue and Chen, Xiaoming and Chung, Yuk Ying and Shen, Yiran},
  journal={IEEE Transactions on Visualization and Computer Graphics},
  year={2024},
  publisher={IEEE}
}

@inproceedings{liang2024perceptual,
  title={Perceptual Quality Assessment of NeRF and Neural View Synthesis Methods for Front-Facing Views},
  author={Liang, Hanxue and Wu, Tianhao and Hanji, Param and Banterle, Francesco and Gao, Hongyun and Mantiuk, Rafal and {\"O}ztireli, Cengiz},
  booktitle={Computer Graphics Forum},
  volume={43},
  number={2},
  pages={e15036},
  year={2024},
  organization={Wiley Online Library}
}
</pre>
