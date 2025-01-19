# Agency IG

This repository is created as a part of the paper "Application of Integrated Gradients Explainability to Sociopsychological Semantic Markers." In this code, the RoBERTa-based Bertagent model, which calculates the agency level of the text, is used. Using the Integrated Gradients package from the Captum library, we extract the attributions of tokens in the text.

For better understanding, we map the RoBERTa tokens to SpaCy tokens, as SpaCy tokens are more similar to word-wise tokenizations. Additionally, for better visualization, we group certain tokens in cases of negations. For example:

## Grouped Negations and Visualization

In cases of negation, tokens are grouped for better attribution visualization. For example:

### Without Grouping Negations

Below is the token-wise attributions without grouping negations. Each token has its color:

<p><span style="background-color: #edf6df;">I</span> <span style="background-color: #f5f7f3;">'m</span> <span style="background-color: #f7f7f6;">nothing</span> <span style="background-color: #f7f7f6;">but</span> <span style="background-color: #f1f6e8;">the</span> <span style="background-color: #488c20;">least</span> <span style="background-color: #549825;">not</span> <span style="background-color: #d9f0bc;">lazy</span> <span style="background-color: #f2f6ec;">person</span> <span style="background-color: #f6f7f5;">.</span></p>

<p><span style="background-color: #f8f2f5;">I</span> <span style="background-color: #f8f2f5;">'m</span> <span style="background-color: #ae106b;">not</span> <span style="background-color: #f7f7f6;">motivated</span> <span style="background-color: #f7f7f7;">.</span></p>

<p><span style="background-color: #f9eff4;">I</span> <span style="background-color: #f8f5f6;">'m</span> <span style="background-color: #f9eff4;">in</span> <span style="background-color: #b1116d;">no</span> <span style="background-color: #f7f7f6;">way</span> <span style="background-color: #f7f7f6;">motivated</span> <span style="background-color: #f7f7f6;">.</span></p>

## Grouped Negations and Visualization

Here’s how the visualization looks:

### Without Grouping Negations
![Without Grouping](images/without_grouping.png)

### With Grouping Negations
![With Grouping](images/with_grouping.png)

This demonstrates the difference between token attributions with and without grouping negations.



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
