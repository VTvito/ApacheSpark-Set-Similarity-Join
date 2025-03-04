# Set Similarity Join with Apache Spark 🚀

## Project Overview
Implementation of Set Similarity Join operations using Apache Spark, focusing on different filtering techniques for large-scale text comparison. Developed and tested on Databricks Community Edition.
Included a step-by-step guide, pipeline version, and tokenization techniques (completed with comments)
and a complete presentation of the project in powerpoint.

## 🛠️ Core Features
- **Advanced Text Processing & Tokenization**
- **Multiple Filtering Techniques:**
  - Length Filtering: `|A ∩ B| ≤ |A| ≤ |B|`
  - Prefix Filtering: Reduces candidate pairs
  - Positional Filtering: Optimizes comparison space
  - Suffix Filtering: Final refinement step
- **Jaccard Similarity Calculation**
- **Performance Optimizations**

## 📁 Repository Structure
```
Spark-Set-Similarity-Join/
├── notebooks/
│   ├── pipeline/
│   │   └── Set_Similarity_Join_with_Spark_Q-3_pipeline.ipynb
│   ├── step_by_step/
│   │   ├── Set_Similarity_Join_with_Spark_Q-3_step_by_step_def.ipynb
│   │   └── Set_Similarity_Join_with_Spark_Q-3_step_by_step_def_ok_100k.ipynb
│   └── tokenization/
│       └── Set_Similarity_Join_with_Spark_word-tokenization_step_by_step_def.ipynb
└── data/
    └── 50KIdDuplicates.json
```

## 🔧 Environment Setup

### Databricks Configuration
1. Access [Databricks Community Edition](https://community.cloud.databricks.com)
2. Create cluster with:
   - Runtime: 13.3 LTS (Apache Spark 3.4.1, Scala 2.12)
   - Python: 3.10
   - Node Type: Standard_DS3_v2

### Required Libraries
```python
dbutils.library.installPyPI("nltk")
dbutils.library.installPyPI("matplotlib")
```

## 📚 Implementation Variants

### 1. Step-by-Step Implementation
- **File**: `notebooks/step_by_step/Set_Similarity_Join_with_Spark_Q-3_step_by_step_def.ipynb`
- Detailed filtering implementations
- Comprehensive explanations
- Perfect for learning purposes

### 2. Pipeline Version
- **File**: `notebooks/pipeline/Set_Similarity_Join_with_Spark_Q-3_pipeline.ipynb`
- Production-ready implementation
- Optimized filter chains

### 3. Large-Scale Version (100k)
- **File**: `notebooks/step_by_step/Set_Similarity_Join_with_Spark_Q-3_step_by_step_def_ok_100k.ipynb`
- Memory-optimized for large datasets
- Enhanced error handling

### 4. Advanced Tokenization
- **File**: `notebooks/tokenization/Set_Similarity_Join_with_Spark_word-tokenization_step_by_step_def.ipynb`
- Advanced text processing
- NLTK integration

## ⚙️ Key Components

### Filtering Techniques
```python
# Length Filtering
def length_filter(tokens1, tokens2, threshold):
    len1, len2 = len(tokens1), len(tokens2)
    return len1 <= len2 and len1 >= len2 * threshold

# Prefix Filtering
def prefix_length(tokens, threshold):
    return len(tokens) - math.ceil(len(tokens) * threshold) + 1

# Positional Filtering
def positional_filter(tokens1, tokens2, pos, threshold):
    required_overlap = math.ceil(threshold * (len(tokens1) + len(tokens2)) / (1 + threshold))
    return len(set(tokens1[:pos]).intersection(tokens2)) >= required_overlap
```

## 📊 Performance Optimization Tips
- Implement filter chain sequence: Length → Prefix → Positional → Suffix
- Use batch processing for large datasets
- Leverage Spark caching strategically
- Monitor memory usage via Databricks metrics

## 🤝 Contributions
Lorenzo Sasso (MSc in Data Engineering UniMore)