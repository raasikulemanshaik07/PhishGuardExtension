
# PhishGuard 🛡️
### Privacy-Focused, Real-Time Phishing Detection for Chromium Browsers

PhishGuard is a browser security extension designed to identify suspicious and potentially malicious URLs using lexical feature analysis, machine learning classification, domain intelligence, and browser-native security mechanisms.

It combines lightweight URL analysis with an in-browser Random Forest classifier to help users identify phishing attempts before interacting with suspicious websites.

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Chromium_Browsers-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Manifest-Version_3-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Detection-Random_Forest-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Privacy-Local_Analysis-purple?style=for-the-badge" />
</p>

<p align="center">
  <b>Analyze suspicious URLs. Detect potential phishing. Make safer browsing decisions.</b>
</p>

---

## 🌐 Project Links

- **Official Website:** [PhishGuard Web](https://raasikulemanshaik07.github.io/PhishGuardWeb/)
- **Browser Extension Repository:** [PhishGuardExtension](https://github.com/raasikulemanshaik07/PhishGuardExtension)
- **Website Repository:** [PhishGuardWeb](https://github.com/raasikulemanshaik07/PhishGuardWeb)

---

## 📌 Overview

Phishing attacks often rely on deceptive URLs, impersonated domains, suspicious subdomains, misleading keywords, and obfuscated web addresses to trick users into revealing sensitive information.

PhishGuard analyzes URL characteristics and evaluates suspicious patterns using a locally executed machine learning model. Its browser-based architecture is designed to minimize dependence on centralized URL-scanning services while providing real-time threat assessment and user-facing warnings.

The extension includes URL analysis, phishing classification, threat warnings, a manual URL scanner, security statistics, and allowlist management.

### Core Objectives

- Identify potentially malicious URLs using lexical and structural characteristics.
- Perform phishing classification locally within the browser.
- Intercept and warn users about URLs classified as suspicious.
- Explain potential indicators of risk.
- Provide a dashboard for manual URL analysis and threat monitoring.
- Reduce unnecessary transmission of browsing information to centralized detection services.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🧠 Machine Learning Detection | Uses a Random Forest classifier for URL classification. |
| ⚡ Local URL Analysis | Extracts URL features and evaluates them within the browser. |
| 🔍 Lexical Feature Engineering | Analyzes URL structure, suspicious tokens, entropy, and other indicators. |
| 🛡️ Threat Warning Interface | Displays warnings when URLs are identified as suspicious. |
| 📊 Security Dashboard | Provides access to security statistics and analysis tools. |
| 🔎 Manual URL Scanner | Allows users to manually inspect a URL. |
| 🌐 Allowlist Management | Supports trusted-domain handling and custom allowlist functionality. |
| 🔄 Model Update Support | Supports updating detection resources without requiring a complete extension replacement. |
| 🔐 Privacy-Focused Design | Avoids sending complete visited URLs to a centralized phishing-classification server for routine local classification. |

---

## 🏗️ Architecture

PhishGuard follows a browser-native architecture using the Chrome Extensions Manifest V3 model.

### Detection Pipeline

```text
                 User Navigates to a URL
                           │
                           ▼
               URL / Navigation Monitoring
                           │
                           ▼
                Trusted-Domain Allowlist
                           │
              ┌────────────┴────────────┐
              │                         │
         Trusted Match             No Trusted Match
              │                         │
              ▼                         ▼
       Allow Navigation          URL Feature Extraction
                                        │
                                        ▼
                                Feature Processing
                                        │
                                        ▼
                              Random Forest Classifier
                                        │
                                        ▼
                               Threat Classification
                                        │
                         ┌──────────────┴──────────────┐
                         │                           │
                    Low-Risk Result              Suspicious Result
                         │                           │
                         ▼                           ▼
                 Continue Navigation          Block / Warning Flow
                                                     │
                                                     ▼
                                             Threat Warning Page
```

### Main Components

- **Background Service Worker:** Handles extension background logic, navigation monitoring, detection workflow, and related security operations.
- **Feature Extraction Engine:** Extracts numerical and categorical indicators from URLs.
- **Random Forest Classifier:** Evaluates extracted features to classify suspicious URLs.
- **Allowlist System:** Handles trusted domains and reduces unnecessary analysis of recognized domains.
- **Threat Warning Interface:** Displays a security warning and analysis details for flagged URLs.
- **Security Dashboard:** Provides manual URL inspection and access to extension security features.
- **Popup Interface:** Provides access to the extension's primary functionality.

---

## 🧠 Machine Learning Model

PhishGuard uses a Random Forest classification model trained to distinguish phishing URLs from legitimate URLs using URL-derived features.

The model is converted into a browser-compatible representation to enable inference using JavaScript without requiring a Python runtime during normal extension operation.

### Why Random Forest?

Random Forest is suitable for URL classification because it:

- Handles non-linear relationships between URL features.
- Captures combinations of suspicious indicators.
- Works effectively with structured numerical features.
- Supports relatively efficient inference.
- Can be deployed without requiring a remote inference API.

A URL may not be suspicious because of a single characteristic. Multiple indicators, such as unusual subdomain depth, suspicious keywords, character distribution, and URL entropy, can collectively contribute to its classification.

---

## 🔬 URL Feature Engineering

PhishGuard evaluates URL characteristics through lexical and structural analysis.

The feature set includes indicators such as:

| Feature Category | Purpose |
|---|---|
| URL Entropy | Identifies unusually random or obfuscated URL patterns. |
| Path Entropy | Evaluates randomness within URL paths. |
| Subdomain Structure | Measures subdomain count and structural complexity. |
| Digit-to-Letter Ratio | Detects unusual numerical patterns. |
| Character Distribution | Evaluates uppercase/lowercase and character patterns. |
| Special Characters | Analyzes characters such as `@`, `-`, `_`, `=`, `?`, and `%`. |
| Suspicious Keywords | Identifies tokens associated with authentication or account manipulation. |
| TLD Indicators | Identifies potentially suspicious top-level domain patterns. |
| IP-Based URLs | Detects URLs using direct IP addresses instead of domain names. |
| Punycode Indicators | Identifies internationalized domain representations that may require scrutiny. |
| Tunneling Indicators | Detects domains associated with tunneling or temporary hosting services. |

These indicators are used as inputs to the classification pipeline rather than treated as standalone proof that a website is malicious.

---

## 🚨 Threat Warning System

When a URL is identified as suspicious, PhishGuard can present a warning interface designed to help users understand the potential risk before proceeding.

The warning interface includes features such as:

- Threat severity indicators.
- Suspicious URL characteristics.
- Detected lexical indicators.
- Technical analysis information.
- Safe navigation options.
- A user-controlled override flow, where supported.

The warning system is intended to provide context rather than simply display a generic block message.

---

## 📊 Security Dashboard

The PhishGuard dashboard provides a centralized interface for interacting with the extension's security functionality.

### Dashboard Capabilities

- View security statistics.
- Review threat-related information.
- Inspect URLs manually.
- View URL analysis results.
- Manage trusted-domain or allowlist entries.
- Access relevant extension controls.

The exact statistics displayed depend on the information maintained by the extension during runtime.

---

## 🔒 Privacy & Data Handling

PhishGuard is designed with a local-first detection approach.

### Local Processing

Routine URL feature extraction and machine learning classification are designed to run locally in the browser. Full visited URLs are not intentionally transmitted to a centralized phishing-classification server as part of the local inference process.

### External Network Requests

Some auxiliary functionality may require external connections, such as:

- Retrieving model or allowlist updates.
- Domain registration information lookups through RDAP services.
- Accessing external resources used by update or intelligence features.

These requests are separate from the local URL classification process and may disclose limited information to the external service involved.

### Privacy Considerations

- Core URL classification is performed locally.
- The extension is designed to avoid centralized URL classification.
- Optional external features may require internet access.
- Users should review the extension's permissions and network-related functionality before installation.

> PhishGuard is privacy-focused, but it should not be described as a completely network-silent extension while external update or domain-intelligence requests remain enabled.

---

## 🌍 Browser Compatibility

PhishGuard is developed for Chromium-based browsers using Manifest V3.

### Primary Target Browsers

| Browser | Support Target |
|---|---|
| Google Chrome | Primary target |
| Microsoft Edge | Chromium-based compatibility |
| Brave | Chromium-based compatibility |
| Opera | Chromium-based compatibility |
| Vivaldi | Chromium-based compatibility |

Compatibility may vary depending on browser version, extension API implementation, permissions, and platform.

Browsers that support Chromium extensions may be compatible, but compatibility should be verified through actual testing before being considered officially supported.

Firefox and Safari are not listed as officially supported targets in this release.

---

## 📥 Installation

PhishGuard can be installed manually using Chrome's extension developer mode.

### Option 1: Download from the Official Website

1. Visit the [PhishGuard Official Website](https://raasikulemanshaik07.github.io/PhishGuardWeb/).
2. Download the extension package provided on the website.
3. Extract the downloaded archive if required.
4. Open the extensions page in your browser.

### Option 2: Download from GitHub

1. Open the [PhishGuardExtension repository](https://github.com/raasikulemanshaik07/PhishGuardExtension).
2. Click the **Code** button.
3. Select **Download ZIP**.
4. Extract the ZIP file to a folder on your computer.

### Load the Extension

#### Google Chrome

Navigate to:

```text
chrome://extensions/
```

#### Microsoft Edge

Navigate to:

```text
edge://extensions/
```

#### Brave

Navigate to:

```text
brave://extensions/
```

#### Opera

Navigate to:

```text
opera://extensions/
```

#### Vivaldi

Navigate to:

```text
vivaldi://extensions/
```

### Installation Steps

1. Open your browser's extensions page.
2. Enable **Developer mode**.
3. Click **Load unpacked**.
4. Select the extracted PhishGuard extension directory containing `manifest.json`.
5. Confirm that PhishGuard appears in your extensions list.
6. Pin the extension to your browser toolbar for convenient access.

---

## 🧪 Model Benchmarking

PhishGuard includes scripts intended for model comparison, performance evaluation, and model export.

The benchmarking workflow is designed to compare multiple machine learning classifiers using URL-derived features and a common dataset.

### Models Evaluated

The comparison framework includes:

- Random Forest
- LightGBM
- XGBoost
- Decision Tree
- Logistic Regression
- Linear Support Vector Machine
- AdaBoost
- Gaussian Naive Bayes

### Evaluation Metrics

| Metric | Purpose |
|---|---|
| Accuracy | Overall proportion of correctly classified samples. |
| Precision | Proportion of predicted phishing samples that are phishing. |
| Recall | Proportion of phishing samples correctly detected. |
| Specificity | Proportion of legitimate samples correctly classified. |
| F1-Score | Harmonic mean of precision and recall. |
| ROC-AUC | Ability to distinguish between classes across thresholds. |
| False Positive Rate | Proportion of legitimate samples incorrectly classified as phishing. |
| Inference Latency | Time required for model inference under the measured conditions. |
| Model Footprint | Size of the model representation. |

### Reported Random Forest Results

The following values are from the project's benchmark documentation and should be interpreted as dataset-specific experimental results, not a guarantee of real-world detection performance.

| Metric | Reported Result |
|---|---:|
| Accuracy | 99.20% |
| Precision | 99.87% |
| Recall | 96.69% |
| Specificity | 99.96% |
| F1-Score | 98.26% |
| ROC-AUC | 99.59% |

> Benchmark results depend on the dataset, data split, feature engineering, training configuration, and test environment. They do not represent guaranteed detection rates against all phishing attacks.

---

## 💻 Running the Benchmark Locally

Benchmarking and model training require Python and the appropriate dependencies.

### Prerequisites

- Python 3.10 or later
- pip
- Git
- Node.js (only for JavaScript benchmarking, if required)

### Clone the Repository

```bash
git clone https://github.com/raasikulemanshaik07/PhishGuardExtension.git
cd PhishGuardExtension
```

### Install Python Dependencies

```bash
pip install scikit-learn pandas numpy matplotlib joblib xgboost lightgbm
```

### Run Model Comparison

```bash
python scripts/compare_models.py
```

On Windows, if you have multiple Python installations:

```powershell
py -3.10 scripts/compare_models.py
```

### Run JavaScript Benchmarking

If the project includes the JavaScript benchmark script and Node.js is installed:

```bash
node scripts/benchmark.js
```

### Retrain and Export the Random Forest Model

If the training script and required dataset are available:

```bash
python train_export_rf.py
```

> The benchmark and training scripts require their corresponding datasets and supporting files. Verify that these resources are present and correctly configured before running the scripts.

---

## 📁 Project Structure

The extension contains browser-facing interfaces, detection logic, model assets, and development or benchmarking resources.

```text
PhishGuardExtension/
│
├── manifest.json
├── background.js
├── content_script.js
│
├── popup.html
├── popup.js
│
├── blocked.html
├── blocked.js
│
├── dashboard.html
├── dashboard.js
│
├── model/
│
├── scripts/
│   ├── compare_models.py
│   └── benchmark.js
│
├── train_export_rf.py
├── README.md
└── LICENSE
```

> This is a representative structure. Files and directories may vary between project versions.

---

## ⚠️ Limitations

PhishGuard is a URL-based detection tool and has limitations.

- A legitimate URL may occasionally be classified as suspicious.
- A phishing URL may evade detection if its characteristics resemble legitimate websites.
- URL lexical analysis alone cannot fully inspect website content, scripts, or server-side behavior.
- Newly created phishing domains may not exhibit obvious suspicious patterns.
- Domain reputation and registration data may be unavailable or incomplete.
- Detection performance can vary across phishing campaigns, datasets, and attack techniques.
- Classification results should not be treated as an absolute guarantee of website safety.

Users should continue to verify website identities, avoid entering credentials on unfamiliar pages, and exercise caution with links received through messages or emails.

---

## 🛠️ Technology Stack

| Technology | Role |
|---|---|
| JavaScript | Browser extension logic and local inference |
| HTML5 | Extension interfaces |
| CSS3 | UI styling |
| Chrome Extensions API | Browser integration |
| Manifest V3 | Extension architecture |
| Python | Model training and evaluation |
| Scikit-learn | Machine learning model development |
| NumPy / Pandas | Data processing |
| Matplotlib | Benchmark visualization |
| Node.js | Optional JavaScript benchmarking |

---

## 🔮 Future Improvements

Potential future enhancements include:

- Improved phishing detection using additional URL and domain features.
- Enhanced explainability for classification decisions.
- More comprehensive testing across browser versions.
- Improved false-positive handling.
- Expanded domain intelligence.
- Reproducible benchmarking and dataset documentation.
- Enhanced dashboard analytics.
- More robust model-update verification and security.

---

## 📄 License

This project is distributed under the license included in the repository.

Please review the `LICENSE` file for licensing terms, usage permissions, attribution requirements, and redistribution conditions.

---

## ⚠️ Disclaimer

PhishGuard is an experimental browser security project intended for educational, research, and defensive purposes.

It is not a replacement for comprehensive browser security, endpoint protection, or professional security solutions. Detection results are probabilistic, and the extension cannot guarantee that every phishing website will be detected or every legitimate website will be correctly classified.

Always verify URLs and exercise caution when sharing personal information online.

---

<p align="center">
  <b>PhishGuard — Safer browsing through local URL intelligence.</b>
</p>
