# Enhanced CSV Processor v1.2

A robust, high-performance CSV processing tool designed for machine learning dataset preparation and data cleaning. This tool specializes in processing various types of datasets including sentiment analysis, coding problems, Q&A pairs, and classification data.

## Features

### Core Capabilities
- **Multi-format Support**: Process CSV files with automatic delimiter detection
- **Advanced Text Cleaning**: Remove HTML entities, normalize whitespace, handle Unicode
- **Duplicate Detection**: Efficient hash-based duplicate removal
- **Data Validation**: Configurable field validation with length constraints
- **Multiple Output Formats**: JSON, TXT, and CSV output options
- **Encoding Detection**: Automatic UTF-8 BOM detection and encoding handling
- **Memory Efficient**: Processes large files without loading entire dataset into memory

### Dataset Types
- **Sentiment Analysis**: Text and sentiment label pairs
- **LeetCode Problems**: Title, difficulty, and description processing
- **Question & Answer**: Q&A pair formatting
- **Classification**: Text categorization datasets
- **Custom**: Flexible schema for any dataset type

### Advanced Features
- **Progress Tracking**: Real-time processing statistics and progress updates
- **Flexible Configuration**: Extensive command-line options for customization
- **Error Handling**: Robust error detection with detailed reporting
- **Performance Optimized**: Handles large datasets efficiently

## Installation

### Prerequisites
- GCC compiler or compatible C compiler
- Standard C library support
- POSIX-compatible system (Linux, macOS, or Windows with MinGW)

### Compilation
```bash
gcc -o csv_processor csv_processor.c -std=c99 -Wall -O2
```

Or with additional optimizations:
```bash
gcc -o csv_processor csv_processor.c -std=c99 -Wall -O3 -march=native
```

## Usage

### Basic Usage
```bash
./csv_processor input.csv --output processed_data.txt
```

### Complete Syntax
```bash
./csv_processor <input_file> --output <output_file> [options]
```

## Command Line Options

### Required Options
- `--output <file>` - Specify output file path

### Dataset Configuration
- `--type <type>` - Dataset type: `sentiment`, `leetcode`, `qa`, `classification`, `custom`
- `--delimiter <char>` - CSV delimiter (auto-detected if not specified)
- `--encoding <enc>` - Input encoding: `utf8`, `latin1`, `auto` (default: auto)
- `--no-header` - Specify that CSV has no header row

### Processing Options
- `--max-lines <n>` - Maximum lines to process (default: 0 = unlimited)
- `--skip-lines <n>` - Skip first n lines (default: 0)
- `--format <fmt>` - Output format: `txt`, `json`, `csv` (default: txt)
- `--train-split <ratio>` - Split ratio for training data (0.0-1.0, default: 0.8)

### Quality Control
- `--strict` - Enable strict validation mode
- `--remove-duplicates` - Remove duplicate entries using hash-based detection
- `--validate` - Enable comprehensive data validation

### Help
- `--help` - Display usage information

## Examples

### Sentiment Analysis Dataset
```bash
./csv_processor reviews.csv --output sentiment_data.txt --type sentiment --remove-duplicates
```

### LeetCode Problems
```bash
./csv_processor problems.csv --output leetcode_clean.json --type leetcode --format json --strict
```

### Custom Dataset with Validation
```bash
./csv_processor data.csv --output clean_data.txt --type custom --validate --max-lines 10000
```

### Processing with Custom Delimiter
```bash
./csv_processor data.tsv --output processed.txt --delimiter $'\t' --no-header
```

## Output Formats

### TXT Format
Human-readable format with clear field separation:
```
Text: This is a sample review
Sentiment: positive
---
```

### JSON Format
Structured JSON objects, one per line:
```json
{"text":"This is a sample review","sentiment":"positive"}
```

### CSV Format
Clean CSV output with proper escaping and formatting.

## Configuration Presets

### Sentiment Analysis
- **Fields**: text, sentiment
- **Validation**: Minimum text length (5 characters)
- **Output**: Text-sentiment pairs

### LeetCode Problems
- **Fields**: title, difficulty, description
- **Validation**: Minimum description length (50 characters)
- **Output**: Structured problem format

### Q&A Pairs
- **Fields**: question, answer
- **Output**: Question-answer format

### Classification
- **Fields**: text, category
- **Output**: Text-category pairs

## Performance Features

### Memory Management
- Efficient string handling with bounds checking
- Dynamic memory allocation for duplicate detection
- Buffer management for large files

### Processing Statistics
The tool provides detailed statistics including:
- Total lines processed
- Error and duplicate counts
- Average text length
- Success rate percentage
- Processing speed

### Example Output
```
=== Processing Statistics ===
Total lines read: 50000
Lines processed: 48500
Lines skipped: 200
Error lines: 800
Duplicate lines: 500
Average text length: 156.3 characters
Success rate: 97.0%
```

## Text Cleaning Features

### HTML Processing
- Decode common HTML entities (`&lt;`, `&gt;`, `&amp;`, `&quot;`, etc.)
- Strip HTML/XML tags
- Handle special characters and Unicode

### Text Normalization
- Remove control characters
- Normalize whitespace
- Trim leading/trailing spaces
- Optional punctuation cleanup in strict mode

### Data Quality
- Handle null/NaN/empty values
- Validate text length requirements
- Remove excessive punctuation (strict mode)

## Error Handling

The processor includes comprehensive error handling:
- File access validation
- Memory allocation checks
- Data format validation
- Graceful handling of malformed CSV lines
- Detailed error reporting with line numbers

## Integration

This tool is designed to work with machine learning pipelines:
```bash
# After processing
./csv_processor data.csv --output training_data.txt
./AryanAi.exe train --data training_data.txt
```

## Technical Specifications

### Limits
- Maximum line length: 8,192 characters
- Maximum fields per line: 32
- Maximum description length: 2,000 characters
- Maximum schema fields: 16
- Buffer size: 65,536 bytes

### Supported Platforms
- Linux (tested)
- macOS (compatible)
- Windows (with MinGW or similar)

## Troubleshooting

### Common Issues

**File not accessible**
```bash
Error: Input file 'data.csv' not accessible: No such file or directory
```
- Verify file path and permissions

**Memory allocation errors**
- Reduce `--max-lines` parameter for very large files
- Ensure sufficient system memory

**Encoding issues**
- Try `--encoding utf8` or `--encoding latin1`
- Check for BOM (Byte Order Mark) in input files

### Performance Tips
- Use `--max-lines` for testing with large files
- Enable `--remove-duplicates` only when necessary
- Use `--strict` mode for highest quality output

## Contributing

This is a standalone C application. To modify or extend:

1. Follow the existing code structure
2. Maintain backwards compatibility
3. Add appropriate error handling
4. Update documentation for new features

