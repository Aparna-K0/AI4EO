# AI4EO
<a id="readme-top"></a>

<div align="center">
  <a href="https://github.com/Aparna-K0/AI4EO">  </a>

  <h3 align="center">Sea Ice and Lead Echo Classification using Unsupervised Learning</h3>

  <p align="center">
    Classifies Sentinel-3 altimetry echoes into sea ice and lead using GMM, calculates average echo shapes, and evaluates against ESA data.
    <br />
    <br />
    <a href="https://github.com/Aparna-K0/AI4EO/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/Aparna-K0/AI4EO/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#dataset">Dataset</a></li>
        <li><a href="#methodology">Methodology</a></li>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#results">Results</a></li>
    <li><a href="#discussion">Discussion</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>

  </ol>
</details>

## About The Project

This project classifies echoes from Sentinel-3 altimetry data into sea ice and lead (open water within sea ice) using unsupervised learning. Accurate classification is vital for various applications like climate monitoring and navigation. The notebook employs Gaussian Mixture Models (GMM) and evaluates performance against official ESA data.  It also generates and visualises average echo shapes and standard deviations for each class.

### Dataset

The project uses Sentinel-3 altimetry data (NetCDF format).  The file should contain:

* `waveform`: Ku-band waveforms.
* `flag`: ESA classification flag (sea ice = 0, lead = 1).
* `sig0`: Normalised radar cross-section.
* `waves`:  (Description of this variable needed - e.g., "Corrected waveforms", "Filtered waveforms", etc.)
* `time_01`, `time_20_ku`, `time_20_c`: Time variables for interpolation.
* `lat`: Latitude of the measurements.
* `lon`: Longitude of the measurements.

**Crucially:** Replace the placeholder path in the notebook (`path`) with your Sentinel-3 data file's actual path.

### Methodology

1. **Data Loading & Preprocessing:**
    * Reads the NetCDF file using `netCDF4`.
    * Unpacks and interpolates variables using `unpack_gpod()`.
    * Calculates Stack Standard Deviation (SSD) using `calculate_SSD()`.
    * Combines features (sig0, peakiness (PP), SSD).
    * Removes rows with NaN values (consider imputation if NaNs are sparse).
    * Standardises features using `StandardScaler`.
    * Filters data based on the ESA flag.

2. **GMM Clustering:**
    * Trains a GMM model (2 components: sea ice, lead).
    * Predicts cluster labels for each echo.

3. **Average Echo Shape Calculation:**
    * Classifies the echoes in leads and sea ice 
    * Calculates average echo shape and standard deviation for each class.

4. **Visualisation:**
    * Plots average echo shapes and standard deviations of both sea ice and leads.
    * Generates scatter plots of clustered data.

5. **Performance Evaluation:**
    * Compares results against ESA data using a confusion matrix and classification report.


### Built With

* Python
* Libraries:
    * `netCDF4`
    * `numpy`
    * `matplotlib`
    * `scikit-learn` (includes `GaussianMixture`, `KMeans`, `StandardScaler`, `MinMaxScaler`)
    * `scipy` (includes `griddata`, `spatial`, `cluster`)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

### Prerequisites

* Python 3
* Required libraries (see Installation)

### Installation

1. Clone the repo:
   ```sh
   git clone [https://github.com/your_github_username/your_repo_name.git](https://www.google.com/search?q=https://github.com/your_github_username/your_repo_name.git)  ```
2. Install required libraries:
   ```sh
   pip install -r requirements.txt  ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

1. **Replace placeholder file path:**  Edit the notebook and replace all `path` variables with your actual file path.
2. **Run the notebook:**  Execute the cells in the notebook sequentially.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Results

The notebook outputs:

* Plots of average echo shapes and standard deviations.
* Confusion matrix and classification report.
* Scatter plots of clustered data.

Analyse the confusion matrix, classification report, and echo shape plots to evaluate the classification performance.

## Discussion

The results are reasonable and the code clearly produces different plots for both sea ice and lead. The lead has a greater mean value. 

## Roadmap

* Investigate unsupervised learning methods including K-means and GMM.
* Use GMM to classify and plot data
* Implement cross-validation.
* Improve NaN handling (e.g., imputation).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Contributions are welcome! Fork the repo, create a feature branch, commit changes, and open a pull request.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

No License 

