# Computational Neuroscience: Neural Modeling and Analysis

This repository presents two complementary computational neuroscience studies: recurrent neural-network simulation and multichannel electrophysiological signal analysis.

The projects were completed individually in a graduate-level computational neuroscience course and have been reorganized here as a technical portfolio. Course instructions and restricted source data are not included.

## Projects

| Notebook                                                                                      | Scope                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Recurrent E–I Neural Network](notebooks/01_recurrent_ei_neural_network.ipynb)                | Simulates a recurrent network of 20 excitatory and 10 inhibitory leaky integrate-and-fire neurons with AMPA/GABA synaptic conductances, examining firing rates, E–I coupling, oscillatory activity, and changes across inhibitory strengths. |
| [Multichannel Neural Signal Analysis](notebooks/02_multichannel_neural_signal_analysis.ipynb) | Analyzes 12-channel tetrode electrophysiological recordings using z-score preprocessing, Pearson correlation, hierarchical and balanced grouping, PCA, FastICA, and Welch power spectral density analysis.                                   |

## 1. Recurrent E–I Neural Network

The model explores how inhibitory strength influences population dynamics in a small recurrent excitatory–inhibitory network.

Mean firing rates during stimulation:

| GABA weight (nS) | Excitatory rate (Hz) | Inhibitory rate (Hz) |
| ---------------- | -------------------: | -------------------: |
| 1.0              |               321.33 |               303.78 |
| 2.0              |               151.83 |               144.44 |
| 4.0              |               133.00 |                79.11 |

At moderate inhibition, the population-rate spectrum shows a dominant peak around **40 Hz**.

The simulation illustrates how changes in inhibitory strength can alter E–I population activity and oscillatory dynamics. Because the model uses simplified LIF neurons, a small network, and no explicit synaptic delays, the resulting firing rates and spectral patterns should be interpreted as properties of the simulation rather than direct physiological estimates.

Cross-correlation at 10 ms resolution indicates strong coupling between excitatory and inhibitory population activity, but does not establish millisecond-scale temporal ordering or a specific biological oscillation mechanism.

### Methods

* Leaky Integrate-and-Fire neuron model
* Recurrent excitatory and inhibitory connectivity
* AMPA and GABA synaptic conductances
* Spike raster and population firing-rate analysis
* Membrane-potential and synaptic-conductance visualization
* E–I cross-correlation
* FFT-based spectral analysis
* Inhibitory-strength parameter sweep

## 2. Multichannel Neural Signal Analysis

The second project analyzes multichannel tetrode recordings and explores whether signal similarity can be used to recover candidate recording groups.

The selected correlation-based groups were:

* Group 1: channels **1, 5, 6, 8**
* Group 2: channels **2, 4, 9, 10**
* Group 3: channels **3, 7, 11, 12**

Mean correlations:

* Within-group correlation: **0.9122**
* Between-group correlation: **0.8085**

Agreement between the correlation-based solution and ICA-based grouping was limited:

* Adjusted Rand Index: **0.0833**
* Best matched overlap: **6 / 12 channels**

Group-averaged spectral peaks occurred at approximately:

* **9.77 Hz**
* **20.02 Hz**
* **20.02 Hz**

The grouping should therefore be interpreted as a candidate organization rather than definitive anatomical identification. Strong shared correlations across channels and weak agreement between grouping methods limit the certainty of the inferred structure.

The analyzed signals are **tetrode extracellular electrophysiological recordings, not EEG**, and this repository does not implement a complete brain-computer interface. The project nevertheless demonstrates analysis methods relevant to neural-signal processing and neurotechnology workflows.

### Methods

* Multichannel neural time-series preprocessing
* Z-score normalization
* Pearson correlation analysis
* Hierarchical clustering
* Balanced channel grouping
* Principal Component Analysis
* Fast Independent Component Analysis
* Component-loading analysis
* Cross-method grouping comparison
* Welch power spectral density analysis

## Technical Stack

* Python
* NumPy
* SciPy
* pandas
* scikit-learn
* Matplotlib
* Jupyter Notebook

## Running Locally

Use Python 3.10 or newer in a virtual environment:

```sh
python -m venv .venv
python -m pip install -r requirements.txt
python -m jupyter lab
```

The recurrent-network simulation is self-contained.

The electrophysiological analysis requires an authorized local copy of the recording data. The original source dataset is not redistributed in this repository. See [data/README.md](data/README.md) for the expected input format.

Notebook outputs are retained so that the main analyses and figures can be inspected without access to the original recording.

## Limitations

These projects were developed as computational neuroscience exercises rather than validated biological or clinical models.

The E–I network uses simplified neuronal and synaptic dynamics, and its quantitative behavior depends strongly on model parameters.

The tetrode analysis does not have independent anatomical ground truth. Correlation-based grouping and ICA capture different statistical properties of the recordings and show only limited agreement in this dataset.

Results should therefore be interpreted as demonstrations of computational modeling and neural-data analysis methodology rather than biological or clinical conclusions.
