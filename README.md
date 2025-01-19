# Agency IG

This repository is created as a part of the paper "Application of Integrated Gradients Explainability to Sociopsychological Semantic Markers." In this code, the RoBERTa-based Bertagent model, which calculates the agency level of the text, is used. Using the Integrated Gradients package from the Captum library, we extract the attributions of tokens in the text.

For better understanding, we map the RoBERTa tokens to SpaCy tokens, as SpaCy tokens are more similar to word-wise tokenizations. Additionally, for better visualization, we group certain tokens in cases of negations. For example:

- Sentence: `I have never been unmotivated!`
  - Grouped tokens: `have never been motivated` will be considered as one token and assigned a single color.

---

## Installments

To use the package, the following libraries are required:

```python
import pandas as pd
import numpy as np
from tqdm.auto import tqdm
import re
!pip install ftfy --quiet
import ftfy
import torch
from torch.utils.data import TensorDataset, DataLoader
from transformers import AutoTokenizer, AutoModelForSequenceClassification
!pip install captum --quiet
from captum.attr import IntegratedGradients
import spacy
from IPython.display import HTML
import matplotlib as mpl
import matplotlib.cm
```

---

## Example Usage

### Define Your Sentences
```python
sentences = [
    "I'm nothing but the least not lazy person.",
    "I'm not motivated.",
    "I'm in no way motivated.",
    "It is not true that I'm nothing but the least not lazy person.",
    "I'm one of the least lazy people you'll ever meet.",
    'I have never been unmotivated!',
    'These people are not lazy at all!'
]
```

### Instantiate and Extract Integrated Gradients
```python
# Instantiate an element for IG inspection
ba0 = AgencyIG()

# Extract IG attributions
ba0.extract_ig(sentences)

# Show the result
for i in range(len(sentences)):
    ba0.render_ig(i)
```

### Get the LaTeX Code
```python
# Show the LaTeX result
for i in range(len(sentences)):
    ba0.latex_render_ig(i)
```

---

## How It Works

Integrated Gradients (IG) is a method for attributing the output of a model to its input features by integrating gradients along a path from a baseline input to the actual input.

For a model \( f \) and input \( x \), the IG of input feature \( i \) is defined as:

$$
\text{IG}_i(x) = (x_i - x_i^0) \times \int_{\alpha=0}^1 \frac{\partial f(x^0 + \alpha \cdot (x - x^0))}{\partial x_i} d\alpha
$$

Where \( x^0 \) is the baseline input.

---

## File Structure

```
/agency-ig/
├── README.md          # Documentation
├── LICENSE            # License file
├── requirements.txt   # Dependencies
├── agency_ig.py       # Main code file
└── examples/
    └── example_usage.py  # Example script
```

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Citation

If you use this code in your research, please cite it as:

```
@misc{agency-ig,
  author = {Your Name},
  title = {Agency IG: Integrated Gradients for NLP Tasks},
  year = {2025},
  howpublished = {\url{https://github.com/yourusername/agency-ig}}
}
```

---

## Contact

For any questions or issues, feel free to open an issue on GitHub or contact [your_email@example.com](mailto:your_email@example.com).
