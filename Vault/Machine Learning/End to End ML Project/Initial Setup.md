## Create a Git Repo 

```bash
git init
```

---
## Creating `venv` project
- Create a `venv` python project by using the following command

```bash
E:\MLproject> conda create -p venv python==3.8 -y
```

- Activate the `venv` project

```bash
E:\MLproject> conda activate venv/
```

---

## `Requirements.txt`

- A text file which basicalyy has all the pakage names you want to import

---

## Setting up a `setup.py` file

- Responsible for **creating ML App** as a ***package*** and deploy it in `python PyPi`
- So, anyone can _install_ and _use_ it

### 🔢 1. Importing the Setup Tools


```python
`from setuptools import setup, find_packages`
```

- `setuptools`: The OG library for building and distributing Python packages.
    
- `find_packages()`: Auto-magically finds all packages/subpackages (folders with `__init__.py`) so you don’t have to list them manually.
    

🧠 Think of it as “automatic folder detective” mode 🕵️

### 🔧 2. The `setup()` Function – Your Project’s DNA

- Let’s zoom in on a sample:

``` python 
setup(     
	name="my_ml_project",
	version="0.1.0",     
	packages=find_packages(where="src"),  # where="src" is optional
	package_dir={"": "src"},     
	install_requires=[         
		"numpy",         
		"pandas",         
		"scikit-learn",
		],     
	author="Jason DAvid",     
	description="An ML project that probably beats ChatGPT in Kaggle",                 long_description=open("README.md").read(),
		long_description_content_type="text/markdown",
		classifiers=[
		    "Programming Language :: Python :: 3",         
		    "Operating System :: OS Independent"
	     ],
	python_requires=">=3.8"
)
```

---

### 💥 Breakdown of Each Part

| Parameter                       | What it Does                                                                                                    |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `name`                          | 📛 Your package’s name on PyPI or locally (`pip install my_ml_project`)                                         |
| `version`                       | 🔢 Your versioning (use semantic versioning like `0.1.0`)                                                       |
| `packages`                      | 📦 Python packages to include (usually `find_packages()`)                                                       |
| `package_dir`                   | 🗂️ Maps root to a folder (`src/` style layout, optional)                                                       |
| `install_requires`              | 📜 List of required 3rd-party packages to auto-install (mostly use a function to fetch from `requirements.txt`) |
| `author`                        | 🧑‍🎨 Your dev name or team (put your name proudly 😤)                                                          |
| `description`                   | 🗣️ Short summary of your project                                                                               |
| `long_description`              | 📘 The README contents (shown on PyPI)                                                                          |
| `long_description_content_type` | ✍️ Markdown or reStructuredText                                                                                 |
| `classifiers`                   | 🔖 Metadata for Python Package Index                                                                            |
| `python_requires`               | 🐍 Sets min Python version to install this                                                                      |

### Bonus 

```txt
HYPHEN_E_DOT = "-e ."
```

### 🤔What's this??
 - This is a special syntax in requirements.txt that tells pip:

1. “Install the current folder (.) as an editable package.”

- Usually used in dev so any changes you make to your source code reflect immediately without reinstalling.

- But setup.py doesn’t want this in install_requires, so we filter it out 🔍

### 📦 3. Function: `get_requirements(file_path)`

```python
def get_requirements(file_path)->List[str]:`
```

- Takes a path to a requirements file and returns a clean list of dependencies.
    

#### 💥 Inside:

> Opens the file 

```python
with open(file_path) as file_obj:
```
#### 🧹Clean-up:

```python
requirements = file_obj.readlines() 

requirements = [req.replace("\n", "") for req in requirements]
```

> Reads all lines and strips that nasty newline char `\n`.

#### Filter:

```python
if HYPHEN_E_DOT in requirements:     requirements.remove(HYPHEN_E_DOT)
```

> 💅 Removes `-e .` so it doesn’t mess up `install_requires`.

### 🧼 Final Polished Version:

``` python
from setuptools import find_packages, setup
from typing import List

HYPHEN_E_DOT = "-e ."

def get_requirements(file_path: str) -> List[str]:
	'''     Reads requirements.txt and returns a list of dependencies     '''          requirements = []     
	
	with open(file_path) as file_obj:  
	# ✅ using the argument now
	     requirements = file_obj.readlines()
	     requirements = [req.strip() for req in requirements]
	     if HYPHEN_E_DOT in requirements:
	         requirements.remove(HYPHEN_E_DOT)
     return requirements`
```

## Install all `dependencies`

- Install all **dependencies** from `requirements.txt` using `pip-install`

```bash
pip install -r requirements.txt
```
