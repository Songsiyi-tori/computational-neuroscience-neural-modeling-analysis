# Local recording input

No recording is distributed in this repository. The signal-analysis notebook retains saved figures and numerical results for inspection.

To execute the analysis, supply a local NumPy `.npy` file that you are authorized to use. The expected input is a numeric matrix with **12 channels × 10,000 samples**, sampled at **1,000 Hz** (10 seconds). A **10,000 × 12** matrix is transposed by the existing preprocessing code. The grouping analysis assumes three tetrodes with four channels each. Sampling rate is an analysis setting and is not inferred from the array.

Set the absolute path before launching Jupyter from the same terminal:

```powershell
# Windows PowerShell
$env:NEURAL_RECORDING_PATH = "C:\private-data\recording.npy"
python -m jupyter lab
```

```sh
# macOS / Linux
export NEURAL_RECORDING_PATH="/absolute/private-data/recording.npy"
python -m jupyter lab
```

Keep the recording outside this repository. The loader disables pickle loading. If no path is configured, it stops with an explanatory error. The network-simulation notebook needs no external recording. Different input data will not reproduce the saved recording-analysis results.
