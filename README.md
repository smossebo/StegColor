# StegColor: High Capacity Text Steganography Using Combinatorial Color Optimization with Huffman Compression


## 📖 Overview

**StegColor** is a novel text steganography framework that achieves **unprecedented embedding capacity** (up to **400%**) through the synergistic integration of:
1. **Combinatorial color optimization** from the 24-bit RGB space (16.7 million colors)
2. **Permutation-based encoding** with dynamic palette selection
3. **Huffman compression** for enhanced capacity and security

This implementation corresponds to the research paper *"High Embedding Capacity Text Steganography Using Optimal Color Combinations from 24-bit Space"*, demonstrating a **17.9× improvement** over state-of-the-art permutation-based methods.

## ✨ Key Features

- **🚀 Ultra-High Capacity**: Embed up to 400% effective capacity (400 bits per 100 characters)
- **🎨 24-bit RGB Combinatorial Space**: Exploit 16,777,216 color combinations
- **📊 Huffman Compression Integration**: 40% average capacity increase + enhanced security
- **🛡️ Adaptive Steganography**: Dynamic parameter adjustment for statistical undetectability
- **📧 Multi-Format Support**: Text, HTML, PDF, and email compatibility
- **⚡ Scalable Implementation**: Linear time complexity O(k·n log n)

## 📊 Performance Comparison

| Method | Effective Capacity | Detection Rate | Coverage | Key Innovation |
|--------|-------------------|----------------|----------|----------------|
| Malik et al. (2017) | 13.43% | 84.2% | ~50% | LZW + Color coding |
| Sadie et al. (2023) | 22.32% | 72.3% | ~45% | Permutation-based |
| **Our Method (no compression)** | **286%** | **53.2%** | **8.4%** | Combinatorial colors |
| **Our Method (with compression)** | **400%** | **37.8%** | **5.9%** | + Huffman compression |

## 🏗️ Architecture

### Core Components:
1. **Combinatorial Color Selection**: Choose optimal n-color subsets from 2²⁴ possibilities
2. **Permutation Encoding**: Encode data using factorial number system ranking
3. **Huffman Compression**: Pre-process messages for enhanced capacity
4. **k-Block Extension**: Scale to arbitrary message lengths
5. **Adaptive Mechanisms**: Dynamic parameter adjustment for undetectability

### Mathematical Foundation:
- Capacity per block: `⌊log₂(C(2²⁴, n) × n!)⌋` bits
- For n=10: **240 bits/block** (vs 21 bits in permutation-only methods)
- With compression: **≈400% effective capacity**

## 📦 Installation

```bash
# Clone repository
git clone https://github.com/smossebo/StegColor.git
cd StegColor

# Install dependencies
pip install -r requirements.txt

# For additional evaluation dependencies
pip install pandas numpy openpyxl matplotlib seaborn xlsxwriter python-docx colorama rich
```

## 🚀 Quick Start

### Basic Usage:
```python
from stegcolor.core import StegColorEncoder

# Initialize encoder
encoder = StegColorEncoder(n_colors=16, use_compression=True)

# Embed secret message
secret_message = "Confidential data to hide"
cover_text = "This is a normal document for covert communication."
stego_text = encoder.embed(secret_message, cover_text)

# Extract message
extracted = encoder.extract(stego_text)
assert extracted == secret_message
```

### Email Integration:
```python
from stegcolor.email_processor import process_email_dataset

# Process Enron email dataset
process_email_dataset(
    input_csv="DatasetsEvaluations/EnronEmailDataset/Spams.csv",
    output_excel="EnronEmailDatasetStego/Spams_Colored.xlsx",
    secret_message="Your secret message here",
    n_colors=16,
    use_compression=True
)
```

## 📁 Repository Structure

```
StegColor/
├── core/                    # Core algorithms
│   ├── encoder.py          # Embedding algorithms
│   ├── decoder.py          # Extraction algorithms
│   ├── huffman.py          # Huffman compression
│   └── combinatorics.py    # Combinatorial utilities
├── evaluation/             # Evaluation scripts
│   ├── new_article_corpus.py
│   ├── enron_email.py
│   ├── arxiv_papers.py
│   └── performance_benchmark.py
├── datasets/              # Sample datasets
│   ├── NewArticleCorpus/
│   ├── EnronEmailDataset/
│   └── arXivData/
├── outputs/              # Generated stego files
│   └── EnronEmailDatasetStego/
├── tests/               # Unit tests
├── requirements.txt     # Dependencies
├── config.yaml         # Configuration
└── README.md
```

## 📊 Evaluation Scripts

The repository includes comprehensive evaluation scripts:

### 1. New Article Corpus Evaluation
```bash
python evaluation/new_article_corpus.py
```
- Processes text files with combinatorial color encoding
- Generates colored Word documents
- Calculates embedding capacity statistics

### 2. Enron Email Dataset Evaluation
```bash
python evaluation/enron_email.py --dataset Nazario --n_colors 16 --compression
```
- Processes email CSV files (Nazario, CEAS, Enron, Ling, NigerianFraud, Spams)
- Creates colored Excel outputs with statistical summaries
- Validates extraction accuracy

### 3. Performance Benchmarking
```bash
python evaluation/performance_benchmark.py --n_range 8 64 --doc_size 10000
```
- Measures runtime vs. number of colors
- Evaluates memory usage
- Compares with baseline methods

## 🧪 Experimental Results

### Embedding Capacity Examples:

**Example 1: Short Message**
- Secret: 35 characters → Compressed to 182 bits
- Cover: 181 characters
- Colors: n=10
- **Result**: 350% effective capacity, 5.5% coverage

**Example 2: Long Message**
- Secret: 200 characters → Compressed to 992 bits
- Cover: 848 characters
- Colors: n=10
- **Result**: 400% effective capacity, 5.9% coverage

### Security Performance:
- **Non-adaptive (no compression)**: 92% detection rate
- **With compression only**: 88% detection rate
- **Adaptive + compression (λ=0.1)**: 15% detection rate
- **Best case (λ=0.2)**: 9% detection rate

## 🔧 Configuration Options

```yaml
# config.yaml
steganography:
  n_colors: 16                    # Colors per block (8-64)
  color_space: 13-bit            # 12-bit, 13-bit, or 24-bit
  adaptive_lambda: 0.1           # Adaptation strength (0-0.3)
  
compression:
  enabled: true
  algorithm: huffman            # huffman, lzw, arithmetic
  target_ratio: 0.62            # Target compression ratio
  dictionary_size: 1024         # Huffman dictionary size
  
performance:
  max_chars: 500                # Characters per processing chunk
  parallel_processing: true
  gpu_acceleration: false
```

## 📈 Advanced Usage

### Adaptive Steganography:
```python
from stegcolor.adaptive import AdaptiveStegColorEncoder

encoder = AdaptiveStegColorEncoder(
    n_colors=24,
    lambda_param=0.1,           # Adaptation strength
    use_compression=True,
    compression_ratio=0.62
)

# Embed with statistical adaptation
stego_text = encoder.embed_adaptive(
    secret_message,
    cover_text,
    adaptation_level="high"     # low, medium, high
)
```

### Multi-Format Export:
```python
from stegcolor.export import MultiFormatExporter

exporter = MultiFormatExporter()
exporter.export_to_word(stego_text, "output.docx")
exporter.export_to_pdf(stego_text, "output.pdf")
exporter.export_to_html(stego_text, "output.html")
```

## 🔬 Research Integration

### Reproducing Paper Results:
```bash
# Run comprehensive experiments
python -m evaluation.comprehensive_experiments \
  --message_sizes 100 500 1000 5000 \
  --color_configs 10 16 24 \
  --compression \
  --output_dir results/
```

### Custom Experiments:
```python
from stegcolor.research import ExperimentRunner

runner = ExperimentRunner()
results = runner.run_experiment(
    dataset="enron",
    n_values=[8, 16, 24, 32],
    message_sizes=[100, 500, 1000],
    compression_levels=[0.5, 0.6, 0.7],
    repetitions=10
)
```

## 📚 Datasets

Download datasets from: [Google Drive](https://drive.google.com/drive/folders/1pN0gyQe2E8Tl7swrgjaa3ktwArDL8r5t?usp=sharing)

Included datasets:
1. **NewArticleCorpus**: News articles for format-based evaluation
2. **Enron Email Dataset**: Real corporate emails for practical testing
3. **arXiv Academic Papers**: Research abstracts for technical content
4. **Compression Test Suite**: Specialized files for compression analysis

## 🧪 Testing

```bash
# Run all tests
pytest tests/ -v

# Test specific modules
pytest tests/test_encoder.py -v
pytest tests/test_huffman.py -v
pytest tests/test_combinatorics.py -v

# Performance tests
pytest tests/performance/ -v --benchmark

