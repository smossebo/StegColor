# README: Color-Based Text Steganography Implementation

## Overview
This Jupyter notebook implements a **color-based text steganography system** that hides secret messages in text documents using color encoding. The system processes multiple datasets and generates steganographic documents with embedded color patterns.

## Features
- **Text Steganography**: Hides messages in text using color combinations and permutations
- **Multiple Output Formats**: Generates colored Word documents (.docx) and Excel files (.xlsx)
- **Dataset Processing**: Processes various text datasets including emails, academic papers, and articles
- **High Capacity**: Uses combinatorial color encoding for increased embedding capacity

## Prerequisites

### Required Python Packages
```bash
pip install python-docx xlsxwriter pandas numpy colorama rich nltk
```

### Required NLTK Data
```python
import nltk
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
nltk.download('stopwords')
```

## Google Drive Setup

### 1. Mount Google Drive
The notebook automatically mounts Google Drive. Ensure you have:
- A Google account with Drive access
- The `DatasetsEvaluations` folder in your MyDrive

### 2. Required Directory Structure
```
MyDrive/
└── DatasetsEvaluations/
    ├── NewArticleCorpus/          # Input text files
    ├── NewArticleCorpusStego/     # Output Word documents
    ├── EnronEmailDataset/         # Email CSV files
    ├── EnronEmailDatasetStego/    # Output Excel files
    ├── arxivAcademicPapers/       # Academic paper datasets
    └── arxivAcademicPapersStego/  # Output files
```

## Dataset Processing

The notebook processes these datasets:

### 1. NewArticleCorpus
- **Input**: Text files (.txt)
- **Output**: Colored Word documents (.docx)
- **Location**: `/content/gdrive/MyDrive/DatasetsEvaluations/NewArticleCorpus`

### 2. Enron Email Datasets
- Nazario.csv, CEAS.csv, Enron.csv, Ling.csv, NigerianFraud.csv, Spams.csv
- **Output**: Colored Excel files (.xlsx)
- **Location**: `/content/gdrive/MyDrive/DatasetsEvaluations/EnronEmailDataset`

### 3. ArXiv Academic Papers
- arxivData.csv, arxivPapers.csv
- **Output**: Colored Excel files (.xlsx)
- **Location**: `/content/gdrive/MyDrive/DatasetsEvaluations/arxivAcademicPapers`

## Running the Notebook

### Step 1: Mount Google Drive
```python
from google.colab import drive
drive.mount('/content/gdrive')
os.chdir('/content/gdrive/MyDrive/DatasetsEvaluations')
```

### Step 2: Execute Main Functions
Run the main processing functions for each dataset:

```python
# Process NewArticleCorpus
main()  # In the "Evaluations NewArticleCorpus" section

# Process Email Datasets
main()  # In each email dataset section (Nazario, CEAS, Enron, etc.)

# Process ArXiv Datasets  
main()  # In each ArXiv dataset section
```

### Step 3: Monitor Output
- Check the output directories for generated files
- Review console output for processing statistics
- Output files will have '_colored' suffix (e.g., `filename_colored.docx`)

## Configuration Parameters

### Secret Message
```python
secret_message = "Coding late into the night, fueled by coffee and a dream to build something amazing that changes everything for good."
```

### Block Size
```python
n = 10  # Number of colors per block
```

### Color Palette
Uses 24 predefined colors including: red, blue, green, yellow, cyan, magenta, orange, purple, brown, gray, etc.

## Output Analysis

### Generated Files
- **Word Documents**: Text with colored characters embedding the secret message
- **Excel Files**: Email bodies with colored text patterns
- **Statistics**: Processing logs with character counts and coloring percentages

### Performance Metrics
- Character coloring percentage
- Processing time per file
- Error handling for corrupt files

## Troubleshooting

### Common Issues

1. **Drive Mounting Errors**
   - Ensure you're logged into Google account
   - Check internet connection
   - Verify Drive storage space

2. **Missing Dependencies**
   - Run all `pip install` commands at the top
   - Restart runtime if packages don't load

3. **File Not Found Errors**
   - Verify directory structure in Google Drive
   - Check file permissions
   - Ensure datasets are in correct folders

4. **Memory Issues**
   - Large datasets may require high-memory runtime
   - Use Google Colab Pro for better performance

### Debug Mode
Enable verbose output by modifying the `process_text_files_in_directory` function to print detailed processing information.

## Technical Details

### Steganography Method
- Uses combinatorial color selection and permutation ranking
- Embeds data in character color patterns
- Maintains text readability while hiding information

### Capacity Calculation
- Block capacity based on color combinations and permutations
- Theoretical capacity: ~11.4x improvement over permutation-only methods

## Output Verification

Check generated files for:
1. **Color Patterns**: Visible color variations in text
2. **File Integrity**: Files open without errors
3. **Message Recovery**: Use extraction algorithm to verify hidden message

## Support
For issues with running the notebook:
1. Check all prerequisite packages are installed
2. Verify Google Drive file structure
3. Ensure sufficient storage space
4. Use Google Colab for cloud execution

## Citation
This implementation is based on color-based text steganography research using combinatorial encoding techniques for high-capacity information hiding.
