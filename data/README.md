# Dataset setup

Use the improved/corrected CIC-IDS2017 release.

Documentation: https://intrusion-detection.distrinet-research.be/CNS2022/CICIDS2017.html

Dataset directory: https://intrusion-detection.distrinet-research.be/CNS2022/Datasets/

Download `CICIDS2017_improved.zip`, extract the day CSV files, and place them locally under:

```text
data/cicids2017_improved/
```

Do **not** commit the raw dataset to GitHub. The repository `.gitignore` excludes it.

The notebook records file hashes, original labels, preprocessing choices, and the treatment of attempted attacks.
