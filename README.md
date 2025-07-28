## Project Organization

```
├── configs             <- config files for logging or other setups
│
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   ├── raw            <- The original, immutable data dump.
│   └── sample         <- Sample data for tests and demos.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│   │                     the creator's initials, and a short `-` delimited description, e.g.
│   │                      `1.0-jqp-initial-data-exploration`.
│   │
│   ├── exploratory/   <- Individual exploration (named with initials)
│   ├── experiments/   <- Structured exps / solid examples out of explorations
│   └── reports/       <- Final polished notebooks to use in presentation/demos
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
└── src                <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes src a Python module
    ├── config.py               <- Store useful variables and configuration
    ├── dataset.py              <- Scripts to download or generate data
    ├── features.py             <- Code to create features for modeling
    ├── modeling                <- Top level modelling, could have several folders for different
    │   │                          modelling practices
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations
│  
├── tests              <- Regular tests
│
├── .env               <- Environment variables go here
├── .gitignore         <- Version control ignore list
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         src and configuration for tools like black
├── README.md          <- The top-level README for developers using this project.
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt` or using pipreqs lib.
│
```
--------


## Git Workflow
### Branch Strategy

1. **Main Branch**: Protected
2. **Feature Branches**: For all work
3. **Naming Convention**: 
   - `type/initials-description-text`
   - `feature/ba-customer-segmentation`
   - `experiment/os-random-forest-baseline`
   - `bugfix/nc-data-loading-error`
   - `eda/cr-target-setting-analysis`


### Simple Git Flow
```bash
# Start
git checkout main
git pull origin main

# Create new branch for your work
git checkout -b feature/your-initials-description

# Work on your code/notebooks
# Add and commit frequently
git add .
git commit -m "Add customer data preprocessing"

# Push your branch
git push -u origin feature/your-initials-description

# Create Pull Request when ready
```

### Pull Request Rules
- **All changes** go through PR (no direct pushes to main)
- **Minimum 1 reviewer** required
- **Clean commit messages**
- **Link to relevant issues/discussions**

## Notebook Management
- Naming: `<step-of-process or number-of-exp>-<user-initials>-<description>.ipynb`
- Example: `0.3-os-visualize-distributions.ipynb`,  `01_reference-date-determination.ipynb`

### Personal Exploration
- Use `notebooks/exploratory/` for EDA
- Commit regularly, don't worry about perfect code

### Structured Experiments
- Use `notebooks/experiments/` for formal experiments or pass from any solid/complete explorations
- These can go through PR review
```bash
# Move promising exploration to experiments
cp notebooks/exploratory/0.1_jd_great_insight.ipynb notebooks/experiments/03_customer_insights.ipynb

# Clean it up, add documentation
# Create PR for review
```
- Clean, well-documented, reproducible


## Code Standards
### Python Code (src/)
```python
# Use docstrings
def preprocess_data(df, config):
    """
    Preprocess raw customer data.
    
    Args:
        df: Raw pandas DataFrame
        config: Configuration dictionary
    
    Returns:
        Processed DataFrame
    """
    pass

# Use type hints
from typing import Dict, List
def load_config(path: str) -> Dict:
    pass
```

### Notebook Standards
```python
# Start with this
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from pathlib import Path

# Set seed for reproducibility
np.random.seed(42)

# Load configuration
import sys
sys.path.append('../src')
from utils.helpers import load_config

config = load_config('../configs/config.yaml')
```

### Configs
- Create a .env file for access keys and secret stuff
```bash
# example .env file
DATABASE_URL=example://username:password@localhost:0000/dbname
ACCESS_KEY=myaccesskey
SECRET_ACCESS_KEY=mysecretkey
OTHER_VARIABLE=something
```
- `src/configs.py` can be used for paths etc.
- `configs/config.yaml` for modelling parameters etc. As it is a yaml format it is both easy to read and set. Multiple configs can be created. Other configs for logging or testing also should be created under `configs/`

## Collaboration Best Practices
### Use issues
- Create Git Issues for:
  - New experiments
  - Bug reports  
  - Feature requests
  - Questions/discussions
- Go over issues in weekly meetings