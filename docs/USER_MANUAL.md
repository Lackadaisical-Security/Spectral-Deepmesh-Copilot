# Deep Translator Engine - User Manual

**Lackadaisical Security 2025**  
**Version:** 1.0.0  
**Date:** August 6, 2025

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Installation Guide](#installation-guide)
3. [Basic Usage](#basic-usage)
4. [Advanced Features](#advanced-features)
5. [Web Interface Guide](#web-interface-guide)
6. [Dataset Management](#dataset-management)
7. [Troubleshooting](#troubleshooting)
8. [FAQ](#faq)

---

## Getting Started

### What is Deep Translator Engine?

The Deep Translator Engine is a professional-grade translation system designed specifically for ancient, constructed, and partially deciphered languages. It combines AI-powered translation with traditional linguistic analysis to provide accurate, confidence-scored translations.

### Key Capabilities

- **Ancient Language Support**: Akkadian, Sumerian, Egyptian hieroglyphs, and more
- **Pattern Recognition**: Detects structural patterns in ancient texts
- **Visual Rendering**: Generate publication-quality SVG images of glyphs
- **Web Interface**: User-friendly browser-based translator
- **Confidence Scoring**: Know how reliable each translation is

---

## Installation Guide

### System Requirements

- **Operating System**: Windows 10+, macOS 10.15+, or Linux
- **Python**: Version 3.11 or higher
- **Memory**: 4GB RAM minimum (8GB recommended)
- **Storage**: 2GB free space for datasets
- **Internet**: Required for OpenAI API access

### Step 1: Download and Setup

1. **Download** the Deep Translator Engine from your source
2. **Extract** to your desired folder (e.g., `C:\DeepTranslator`)
3. **Open** command prompt/terminal in the project folder

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

This installs all required Python packages.

### Step 3: Configure API Access

1. **Get an OpenAI API key** from https://platform.openai.com
2. **Set environment variable**:

Windows:
```cmd
set OPENAI_API_KEY=your_api_key_here
```

Mac/Linux:
```bash
export OPENAI_API_KEY=your_api_key_here
```

3. **Test the installation**:
```bash
python -c "from deep_translator_engine import DeepTranslatorEngine; print('Installation successful!')"
```

---

## Basic Usage

### Using the Web Interface (Recommended)

1. **Start the web server**:
```bash
python -m deep_translator_engine.frontend.server
```

2. **Open your browser** to: `http://localhost:8000`

3. **Load a dataset**:
   - Drag and drop a dataset file (ZIP, JSON, or CSV)
   - Wait for "Dataset loaded successfully" message

4. **Translate text**:
   - Enter ancient script symbols in the input field
   - Select input type (Symbol ID, Phonetic Form, or English Gloss)
   - Click "Translate" to see results

### Using Python Code

```python
from deep_translator_engine import DeepTranslatorEngine

# Initialize the engine
engine = DeepTranslatorEngine()

# Load a dataset
success = engine.load_dataset('data/akkadian_lexicon.zip')
if success:
    print("Dataset loaded successfully!")

# Translate a symbol
result = engine.translate("𒀭", input_type="symbol_id")
print(f"Translation: {result.translation}")
print(f"Confidence: {result.confidence:.1%}")
```

---

## Advanced Features

### Pattern Recognition

The engine can detect structural patterns in ancient texts:

```python
from deep_translator_engine import PatternMatcher

matcher = PatternMatcher()

# Analyze a sequence of symbols
symbols = ["𒀭", "𒈗", "𒆤", "𒀭", "𒈗", "𒆤"]
analysis = matcher.detect_patterns(symbols)

print(f"Found {len(analysis.detected)} patterns:")
for pattern in analysis.detected:
    print(f"- {pattern.type}: {pattern.confidence:.1%} confidence")
```

### SVG Glyph Rendering

Create publication-quality images of ancient scripts:

```python
from deep_translator_engine import SVGRenderer, RenderingStyle

renderer = SVGRenderer()

# Render a single glyph
svg_content = renderer.render_glyph("𒀭", style=RenderingStyle.SCHOLARLY)

# Save to file
with open("glyph.svg", "w") as f:
    f.write(svg_content)
```

Available rendering styles:
- **Basic**: Clean, simple representation
- **Artistic**: Decorative styling
- **Scholarly**: Academic format with annotations
- **Cuneiform**: Specialized for cuneiform scripts
- **Hieroglyphic**: Egyptian hieroglyph styling

### Confidence Analysis

Understanding translation reliability:

```python
result = engine.translate("complex_text", input_type="phonetic_form")

print(f"Primary translation: {result.translation}")
print(f"Confidence level: {result.confidence:.1%}")

if result.confidence < 0.7:
    print("Low confidence - consider alternatives:")
    for alt in result.alternatives:
        print(f"  - {alt}")
```

---

## Web Interface Guide

### Main Interface Components

1. **Dataset Panel** (Top Left)
   - Drag-and-drop area for dataset files
   - Shows currently loaded dataset name
   - Displays dataset statistics

2. **Input Panel** (Top Right)
   - Text input field for symbols/text
   - Input type selector dropdown
   - Translate button

3. **Results Panel** (Bottom Left)
   - Primary translation display
   - Confidence score with color coding
   - Alternative translations list

4. **Visualization Panel** (Bottom Right)
   - SVG rendering of input symbols
   - Style selector for different rendering modes
   - Export button for saving images

### Dataset Loading

**Supported formats:**
- **ZIP files**: Complete language packages
- **JSON files**: Structured lexicon data
- **CSV files**: Tabular symbol mappings

**Loading process:**
1. Prepare your dataset file
2. Drag the file to the "Drop dataset here" area
3. Wait for parsing (may take 10-30 seconds for large files)
4. Look for "Dataset loaded successfully" confirmation

### Translation Workflow

1. **Select input type**:
   - **Symbol ID**: Ancient script characters (𒀭, 𓂀, ᚱ)
   - **Phonetic Form**: Transliteration (lugal, ankh, raidho)
   - **English Gloss**: English meanings (king, life, journey)

2. **Enter text**: Type or paste your content

3. **Translate**: Click the translate button

4. **Review results**:
   - Check confidence score (green = high, yellow = medium, red = low)
   - Consider alternatives for low-confidence translations
   - View pattern analysis if detected

---

## Dataset Management

### Dataset Structure

Datasets should follow this general structure:

```json
{
  "metadata": {
    "name": "Akkadian Lexicon",
    "language": "akkadian",
    "script": "cuneiform",
    "version": "1.0"
  },
  "symbols": [
    {
      "id": "AK_001",
      "symbol": "𒀭",
      "gloss": "god, divine",
      "transliteration": "AN",
      "context": "religious texts",
      "frequency": "high"
    }
  ]
}
```

### Creating Custom Datasets

1. **Prepare your data** in CSV format:
```csv
symbol,gloss,transliteration,context
𒀭,god,AN,religious
𒈗,king,LUGAL,royal titles
𒆤,ox,GUD,animals
```

2. **Convert to JSON** (optional but recommended):
```python
import pandas as pd
import json

# Load CSV
df = pd.read_csv('my_lexicon.csv')

# Convert to engine format
dataset = {
    "metadata": {
        "name": "My Custom Lexicon",
        "language": "custom"
    },
    "symbols": df.to_dict('records')
}

# Save as JSON
with open('my_lexicon.json', 'w') as f:
    json.dump(dataset, f, indent=2)
```

### Working with ZIP Archives

For complex datasets with multiple files:

1. **Create folder structure**:
```
my_dataset/
├── lexicon.json
├── grammar_rules.json
├── pattern_examples.json
└── metadata.json
```

2. **Compress to ZIP**: Use any ZIP utility

3. **Load in engine**: Drag-and-drop the ZIP file

---

## Troubleshooting

### Common Issues

**Problem**: "Dataset failed to load"
**Solution**: 
- Check file format (must be ZIP, JSON, or CSV)
- Verify file is not corrupted
- Ensure proper column names in CSV files

**Problem**: "API connection failed"
**Solution**:
- Verify OpenAI API key is set correctly
- Check internet connection
- Confirm API key has o3 model access

**Problem**: "Low confidence translations"
**Solution**:
- Try alternative input types
- Check for typos in input text
- Consider loading additional datasets for context

**Problem**: "Web interface won't load"
**Solution**:
- Ensure port 8000 is available
- Try different browser
- Check firewall settings

### Debug Mode

Enable detailed logging:

```python
import logging
logging.basicConfig(level=logging.DEBUG)

engine = DeepTranslatorEngine()
# Now all operations will show debug information
```

### Performance Issues

**Slow translations**:
- Reduce `max_tokens` in configuration
- Disable pattern analysis for simple translations
- Use smaller datasets

**High memory usage**:
- Load datasets one at a time
- Clear cache periodically
- Reduce batch processing size

---

## FAQ

**Q: What languages are supported?**
A: The engine supports any language with available datasets. Pre-configured support includes Akkadian, Sumerian, Ancient Greek, Egyptian Hieroglyphs, Norse Runes, and many constructed languages.

**Q: Can I use this offline?**
A: No, the engine requires internet access for OpenAI API calls. However, dataset loading and SVG rendering work offline.

**Q: How accurate are the translations?**
A: Accuracy varies by language and text complexity. The confidence score indicates reliability - scores above 80% are generally very reliable, 60-80% are good, below 60% should be verified.

**Q: Can I add my own languages?**
A: Yes! Create datasets following the documented format and load them through the interface.

**Q: Is this suitable for academic research?**
A: Yes, the engine includes citation tracking, confidence scoring, and scholarly rendering modes designed for academic use.

**Q: What's the difference between MIT and LQX-20 licenses?**
A: MIT license covers open-source, educational, and personal use. LQX-20 covers commercial applications and enterprise deployment.

**Q: How do I report bugs or request features?**
A: Contact support@lackadaisical-security.com or linguistics@lackadaisical-security.com

**Q: Can I integrate this into my own application?**
A: Yes, the engine provides comprehensive APIs for integration. See the API Reference Guide for details.

---

## Support

**Technical Support**: support@lackadaisical-security.com  
**Linguistic Consultation**: linguistics@lackadaisical-security.com  
**Website**: https://lackadaisical-security.com  
**Documentation**: Full API reference available in docs/

---

**© 2025 Lackadaisical Security. All rights reserved.**
