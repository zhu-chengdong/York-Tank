# York-Tank

**York-Tank: A Degradation-Aware and Difficulty-Stratified Stereo Dataset for Underwater Visual SLAM**

York-Tank is a controlled underwater stereo dataset for studying how visual degradations affect SLAM tracking, localization, and failure behavior. Its 16 sequences share a controlled tank scene and are organized by dominant degradation factor and difficulty.

**Dataset release:** The complete 16-sequence dataset is publicly available on Zenodo as **v2**, under [DOI 10.5281/zenodo.23347574](https://doi.org/10.5281/zenodo.23347574).

**Paper status:** The associated paper has been accepted by *Sensors* (2026).

## Dataset overview

- **16 sequences** and **18,948 synchronized stereo image pairs** (approximately 15.8 minutes).
- Rectified grayscale stereo images, **1280 × 800** pixels, recorded at **20 Hz**.
- Five degradation factors: **low illumination**, **non-uniform illumination**, **fast motion**, **texture deficiency**, and **dynamic interference**.
- Four difficulty levels: **Level 1** (two baseline sequences), **Level 2** (five easy single-degradation sequences), **Level 3** (five hard single-degradation sequences), and **Level 4** (four hybrid-degradation sequences).
- Stereo images, IMU measurements, calibration files, raw AprilTag-array reference poses, and ROS bag files.

## Data availability

| Release | Status | Link |
| --- | --- | --- |
| **Complete 16-sequence release (v2)** | **Publicly available** | [Zenodo complete dataset (10.5281/zenodo.23347574)](https://doi.org/10.5281/zenodo.23347574) |
| Earlier Sequence 1 preview (v1) | Publicly available | [Zenodo preview (10.5281/zenodo.20432375)](https://doi.org/10.5281/zenodo.20432375) |

The complete release contains **16 sequence TAR archives** and **`York-Tank-Support.tar`**, totaling approximately **51.1 GB**. Use the v2 record above to download the complete dataset. The earlier v1 record contains only the Sequence 1 preview.

## Sequences

| Sequence | Primary condition | Difficulty | Stereo pairs |
| --- | --- | --- | ---: |
| `1_reference1` | Baseline | Level 1 | 1,339 |
| `2_reference2` | Baseline | Level 1 | 1,235 |
| `3_dark_easy` | Low illumination | Level 2 | 1,234 |
| `4_dark_hard` | Low illumination | Level 3 | 1,452 |
| `5_uneven_easy` | Non-uniform illumination | Level 2 | 1,237 |
| `6_uneven_hard` | Non-uniform illumination | Level 3 | 1,179 |
| `7_fastmotion_easy` | Fast motion | Level 2 | 1,157 |
| `8_fastmotion_hard` | Fast motion | Level 3 | 1,330 |
| `9_fewtexture_easy` | Texture deficiency | Level 2 | 1,184 |
| `10_fewtexture_hard` | Texture deficiency | Level 3 | 1,310 |
| `11_dynamic_easy` | Dynamic interference | Level 2 | 1,151 |
| `12_dynamic_hard` | Dynamic interference | Level 3 | 1,205 |
| `13_hybrid` | Hybrid degradation | Level 4 | 902 |
| `14_hybrid` | Hybrid degradation | Level 4 | 1,198 |
| `15_hybrid` | Hybrid degradation | Level 4 | 931 |
| `16_hybrid` | Hybrid degradation | Level 4 | 904 |
| **Total** | | | **18,948** |

An earlier development version contained 18 sequences, including two bright-illumination sequences. Those two were excluded from the final *Sensors* benchmark, and the remaining sequences were renumbered as shown above.

## Release organization

Each sequence TAR archive contains its `sequences/<sequence>/` directory and corresponding `rosbags/<sequence>.bag`. `York-Tank-Support.tar` contains the README, license, checksums, sequence manifest, calibration files, documentation, and basic data access and integrity-checking scripts.

Extract the archives into the **same destination directory**. Extracting all 17 archives reconstructs the following layout:

```text
York-Tank-Release/
├── README.md
├── LICENSE
├── SHA256SUMS
├── sequence_manifest.csv
├── calibration/
├── docs/
├── scripts/
├── sequences/
│   ├── 1_reference1/
│   │   ├── left/
│   │   ├── right/
│   │   ├── imu.csv
│   │   ├── gt/groundtruth.txt
│   │   └── metadata.yaml
│   └── ... (through 16_hybrid)
└── rosbags/
    ├── 1_reference1.bag
    └── ... (through 16_hybrid)
```

The ROS bag image topics are:

- `/camera/left/image_rect_underwater`
- `/camera/right/image_rect_underwater`

The left/right images have matching timestamps. The sequence manifest lists sequence identities and counts and documents reference-trajectory time coverage.

### Reference trajectory convention

**Important:** The provided `gt/groundtruth.txt` files contain **raw AprilTag-array poses expressed in the fixed overhead-camera frame**. They must **not** be interpreted directly as onboard left-camera poses. A fixed transformation from the AprilTag array to the left camera is required for camera-frame trajectory evaluation; that transformation is **not included as a verified, ready-to-use conversion** in the published release.

Some image timestamps fall outside the reference trajectory's temporal coverage. In particular, this affects `6_uneven_hard`, `9_fewtexture_easy`, and `10_fewtexture_hard`. Images have been retained; consult `sequence_manifest.csv` for the relevant intervals. For ATE evaluation, use consistent coordinate frames and only temporally associated poses.

## Associated publication

Chengdong Zhu and Mark Post, “York-Tank: A Degradation-Aware and Difficulty-Stratified Stereo Dataset for Underwater Visual SLAM,” *Sensors*, accepted in 2026. Journal DOI and final bibliographic details will be added when available.

## Dataset citation

Chengdong Zhu (2026). *York-Tank: A Degradation-Aware and Difficulty-Stratified Stereo Dataset for Underwater Visual SLAM* (v2) [Data set]. Zenodo. [https://doi.org/10.5281/zenodo.23347574](https://doi.org/10.5281/zenodo.23347574).

## License and contact

The dataset and accompanying materials are licensed under **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)**. See `LICENSE` in `York-Tank-Support.tar`.

**Chengdong Zhu**  
Department of Electronic Engineering, University of York, United Kingdom  
chengdong.zhu@york.ac.uk
