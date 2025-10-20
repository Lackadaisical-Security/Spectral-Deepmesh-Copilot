# API Reference Guide

**Deep Translator Engine v1.0.0**  
**Lackadaisical Security 2025**

---

## Table of Contents

1. [Engine Orchestrator](#engine-orchestrator)
2. [Dataset Management](#dataset-management)
3. [Core Translation](#core-translation)
4. [Pattern Recognition](#pattern-recognition)
5. [Confidence System](#confidence-system)
6. [SVG Rendering](#svg-rendering)
7. [Web Frontend](#web-frontend)
8. [Configuration](#configuration)
9. [Error Handling](#error-handling)
10. [Examples](#examples)

---

## Engine Orchestrator

### `DeepTranslatorEngine`

Main orchestrator class that coordinates all engine components.

```python
class DeepTranslatorEngine:
    """Production-ready deep translator engine."""
    
    def __init__(self, config_path: Optional[str] = None):
        """Initialize engine with optional configuration."""
        
    def get_status(self) -> Dict[str, Any]:
        """Get comprehensive engine status."""
        
    def load_dataset(self, path: str, format_hint: Optional[str] = None) -> bool:
        """Load translation dataset from file."""
        
    def translate(self, text: str, input_type: str = "auto", **options) -> TranslationResult:
        """Translate text with confidence scoring."""
```

**Parameters:**
- `config_path`: Optional path to configuration file
- `text`: Input text to translate
- `input_type`: One of `"symbol_id"`, `"phonetic_form"`, `"english_gloss"`, `"auto"`
- `options`: Additional translation parameters

**Returns:** `TranslationResult` object with translation data

---

## Dataset Management

### `DatasetLoader`

Handles loading and parsing of translation datasets.

```python
class DatasetLoader:
    """Multi-format dataset ingestion system."""
    
    def load_from_file(self, file_path: str) -> LoadResult:
        """Load dataset from ZIP, JSON, or CSV file."""
        
    def validate_dataset(self, data: Dict[str, Any]) -> ValidationResult:
        """Validate dataset structure and content."""
        
    def get_supported_formats(self) -> List[str]:
        """Get list of supported dataset formats."""
```

**Supported Formats:**
- **ZIP Archives**: Multiple files with lexicon data
- **JSON**: Structured symbol mappings
- **CSV**: Tabular data with flexible column mapping

---

## Core Translation

### `Translator`

Bidirectional translation engine with OpenAI integration.

```python
class Translator:
    """Core translation engine with OpenAI o3 integration."""
    
    def translate_symbol_id(self, symbol_id: str, context: Dict[str, Any]) -> TranslationResult:
        """Translate symbol ID to gloss/transliteration."""
        
    def translate_gloss(self, gloss: str, target_script: str) -> TranslationResult:
        """Translate English gloss to target script."""
        
    def get_alternatives(self, text: str, max_results: int = 5) -> List[TranslationResult]:
        """Get alternative translations with confidence scores."""
```

### `TranslationResult`

Container for translation output with metadata.

```python
class TranslationResult:
    """Translation result with confidence and metadata."""
    
    translation: str              # Primary translation
    confidence: float             # Confidence score (0.0-1.0)
    alternatives: List[str]       # Alternative translations
    source_citation: str          # Data source reference
    metadata: Dict[str, Any]      # Additional context
    processing_time: float        # Translation duration
```

---

## Pattern Recognition

### `PatternMatcher`

Advanced structural pattern detection for ancient texts.

```python
class PatternMatcher:
    """Structural pattern detection and analysis."""
    
    def detect_patterns(self, sequence: List[str]) -> PatternAnalysis:
        """Analyze sequence for structural patterns."""
        
    def find_chant_cycles(self, symbols: List[str]) -> List[ChantCycle]:
        """Detect repetitive chant patterns."""
        
    def analyze_genealogy(self, text: str) -> GenealogyPattern:
        """Identify genealogical relationship patterns."""
        
    def detect_creation_triads(self, symbols: List[str]) -> List[CreationTriad]:
        """Find creation mythology triadic structures."""
```

### Pattern Types

```python
class PatternType(Enum):
    CHANT_CYCLE = "chant_cycle"
    GENEALOGY = "genealogy"
    CREATION_TRIAD = "creation_triad"
    CYCLIC_FORMATION = "cyclic_formation"
    SEQUENTIAL = "sequential"
```

---

## Confidence System

### `ConfidenceCalculator`

Advanced confidence scoring with multi-source validation.

```python
class ConfidenceCalculator:
    """Multi-source confidence calculation system."""
    
    def calculate_confidence(self, translation: str, sources: List[Source]) -> float:
        """Calculate weighted confidence score."""
        
    def validate_multi_source(self, results: List[TranslationResult]) -> ValidationMetrics:
        """Validate translation across multiple sources."""
        
    def get_quality_metrics(self, dataset_id: str) -> QualityMetrics:
        """Get quality assessment for dataset."""
```

### Confidence Factors

```python
class ConfidenceFactor(Enum):
    SOURCE_RELIABILITY = "source_reliability"
    PATTERN_CONSISTENCY = "pattern_consistency"
    LINGUISTIC_COHERENCE = "linguistic_coherence"
    HISTORICAL_ACCURACY = "historical_accuracy"
    CROSS_REFERENCE_MATCH = "cross_reference_match"
```

---

## SVG Rendering

### `SVGRenderer`

Glyph visualization system with multiple rendering styles.

```python
class SVGRenderer:
    """Professional glyph visualization system."""
    
    def render_glyph(self, symbol: str, style: RenderingStyle = RenderingStyle.BASIC) -> str:
        """Render single glyph as SVG."""
        
    def render_sequence(self, symbols: List[str], layout: LayoutType = LayoutType.HORIZONTAL) -> str:
        """Render symbol sequence with layout options."""
        
    def batch_export(self, symbol_dict: Dict[str, str], output_dir: str) -> BatchExportResult:
        """Export multiple glyphs to SVG files."""
```

### Rendering Styles

```python
class RenderingStyle(Enum):
    BASIC = "basic"
    ARTISTIC = "artistic"  
    SCHOLARLY = "scholarly"
    CUNEIFORM = "cuneiform"
    HIEROGLYPHIC = "hieroglyphic"
    RUNIC = "runic"
    LINEAR = "linear"
```

### Layout Options

```python
class LayoutType(Enum):
    HORIZONTAL = "horizontal"
    VERTICAL = "vertical"
    GRID = "grid"
```

---

## Web Frontend

### Frontend API

JavaScript interface for web-based interaction.

```javascript
class TranslatorAPI {
    /**
     * Initialize translator interface
     */
    constructor(baseUrl = '/api') {
        this.baseUrl = baseUrl;
    }
    
    /**
     * Load dataset via drag-and-drop
     */
    async loadDataset(file) {
        // Implementation details
    }
    
    /**
     * Translate text with live updates
     */
    async translate(text, options = {}) {
        // Returns translation result
    }
    
    /**
     * Render glyph visualization
     */
    async renderGlyph(symbol, style = 'basic') {
        // Returns SVG string
    }
}
```

---

## Configuration

### Settings Structure

```yaml
# Main configuration file: config/settings.yaml

# OpenAI API Configuration
openai:
  api_key: ${OPENAI_API_KEY}
  model: "gpt-4o-deep-research"
  temperature: 0.3
  max_tokens: 2000
  timeout: 30

# Translation Settings  
translation:
  confidence_threshold: 0.7
  max_alternatives: 5
  enable_pattern_analysis: true
  bidirectional: true

# Dataset Configuration
datasets:
  data_path: "./data/"
  supported_formats: ["json", "csv", "zip"]
  auto_validation: true
  cache_results: true

# Logging Configuration
logging:
  level: INFO
  file: "logs/translator.log"
  format: "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
  max_size: "10MB"
  backup_count: 5

# SVG Rendering
svg:
  default_style: "basic"
  output_width: 200
  output_height: 200
  include_metadata: true
```

---

## Error Handling

### Exception Types

```python
class TranslationError(Exception):
    """Base exception for translation errors."""
    pass

class DatasetLoadError(TranslationError):
    """Dataset loading/parsing errors."""
    pass

class APIConnectionError(TranslationError):
    """OpenAI API connection errors."""
    pass

class ConfidenceThresholdError(TranslationError):
    """Translation confidence below threshold."""
    pass

class PatternRecognitionError(TranslationError):
    """Pattern analysis errors."""
    pass

class SVGRenderError(TranslationError):
    """SVG generation errors."""
    pass
```

### Error Response Format

```python
class ErrorResponse:
    """Standardized error response format."""
    
    error_code: str          # Error classification
    message: str             # Human-readable message
    details: Dict[str, Any]  # Additional error context
    timestamp: datetime      # Error occurrence time
    request_id: str          # Request identifier
```

---

## Examples

### Basic Translation

```python
from deep_translator_engine import DeepTranslatorEngine

# Initialize engine
engine = DeepTranslatorEngine()

# Load dataset
engine.load_dataset('data/akkadian_lexicon.zip')

# Translate symbol
result = engine.translate("𒀭", input_type="symbol_id")
print(f"Translation: {result.translation}")
print(f"Confidence: {result.confidence:.2%}")
print(f"Alternatives: {result.alternatives}")
```

### Pattern Analysis

```python
from deep_translator_engine import PatternMatcher

matcher = PatternMatcher()

# Analyze sequence for patterns
symbols = ["𒀭", "𒈗", "𒆤", "𒀭", "𒈗", "𒆤"]
patterns = matcher.detect_patterns(symbols)

for pattern in patterns.detected:
    print(f"Pattern: {pattern.type}")
    print(f"Confidence: {pattern.confidence:.2%}")
```

### SVG Rendering

```python
from deep_translator_engine import SVGRenderer, RenderingStyle

renderer = SVGRenderer()

# Render single glyph
svg_output = renderer.render_glyph("𒀭", style=RenderingStyle.CUNEIFORM)

# Render sequence
sequence = ["𒀭", "𒈗", "𒆤"]
svg_sequence = renderer.render_sequence(sequence, layout=LayoutType.HORIZONTAL)

# Batch export
symbols = {"AN": "𒀭", "LUGAL": "𒈗", "GUD": "𒆤"}
result = renderer.batch_export(symbols, "output/glyphs/")
```

### Web Interface Integration

```html
<!DOCTYPE html>
<html>
<head>
    <title>Deep Translator Engine</title>
    <script src="js/translator-api.js"></script>
</head>
<body>
    <script>
        const api = new TranslatorAPI();
        
        // Load dataset
        document.getElementById('file-input').addEventListener('change', async (e) => {
            const result = await api.loadDataset(e.target.files[0]);
            console.log('Dataset loaded:', result.success);
        });
        
        // Translate text
        async function translateText(input) {
            const result = await api.translate(input);
            document.getElementById('output').textContent = result.translation;
            document.getElementById('confidence').textContent = `${result.confidence}%`;
        }
    </script>
</body>
</html>
```

---

## Testing

### Running Tests

```bash
# Run all tests
pytest

# Run specific component tests
pytest tests/test_translator.py -v

# Run with coverage
pytest --cov=deep_translator_engine --cov-report=html

# Current status: 68/68 tests passing
```

### Test Categories

- **Unit Tests**: Individual component functionality
- **Integration Tests**: Cross-component interaction
- **Frontend Tests**: Web interface validation
- **Dataset Tests**: Data loading/parsing verification
- **API Tests**: External service integration
- **Performance Tests**: Speed and memory optimization

---

**Version:** 1.0.0  
**Last Updated:** August 6, 2025  
**Status:** Production Ready (68/68 tests passing)

**© 2025 Lackadaisical Security. All rights reserved.**
