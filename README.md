# GW150914-Python-Analysis

### **Overview**
This repository contains a modernized, streamlined Python analysis of the first direct detection of gravitational waves, GW150914. 

The original 2015 tutorials often relied on manual data downloads, JSON parameter files, and custom scripts like `readligo.py`. This project updates that workflow for the modern era, utilizing `gwpy` and `gwosc` to stream Advanced LIGO data directly from the server and process the signal with optimized, built-in methods.

### **Key Features & Modernizations**
* **Direct Data Streaming:** Eliminates the need for manual HDF5/JSON downloads by querying the LIGO database directly for GPS times and strain data.
* **Dynamic Sampling:** Extracts the temporal resolution (4096 Hz) straight from the fetched time series to ensure Nyquist-Shannon compliance.
* **Built-in Spectral Analysis:** Replaces manual Fourier transforms and interpolation with `gwpy`'s native `.asd()` and `.whiten()` methods to estimate noise and clean the signal.
* **BNS Detection Range:** Calculates the horizon distance for a standard Binary Neutron Star merger at the time of the event.

### **The Physics Breakdown**
This notebook walks through the standard signal processing pipeline to pull a gravitational wave "chirp" out of heavy background noise:

1. **The Measurement:** Gravitational waves are ripples in spacetime curvature. LIGO measures this as a dimensionless strain, $h(t)$, by looking at the difference in length between its 4 km arms. A strain of $10^{-21}$ corresponds to a length change 1,000 times smaller than a proton.
2. **Amplitude Spectral Density (ASD):** The signal is buried in noise. The ASD plots the detector's sensitivity across frequencies, showing the "Seismic Wall" at low frequencies, Quantum Shot Noise at high frequencies, and the sensitive "bucket" in the middle where the black holes merged.
3. **Whitening:** The raw data is divided by the ASD curve. This "turns down the volume" on dominant seismic and thermal noise, creating a flat noise floor where the chirp can be seen.

### **Installation & Setup**
To run this notebook locally, you will need standard scientific Python libraries along with the LIGO-specific packages. 

```bash
pip install numpy scipy matplotlib gwpy gwosc
```

### **Usage**
Simply open the `gw150914.ipynb` notebook and run the cells sequentially. The script will automatically fetch the 32-second data segment centered on GW150914 and generate the corresponding plots.

### **License**
This project is open-source and available under the **MIT License**.
