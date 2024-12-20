# Guide to Python Environments: `requirements.txt` vs `environment.yml`

Managing environments is a crucial part of Python development. This guide explains the usage, purpose, and differences between `requirements.txt` (for `pip`) and `environment.yml` (for `conda`) to help you choose the right tool for your project.

---

## 1. **Introduction to `requirements.txt`**

`requirements.txt` is a simple file used to list Python package dependencies for installation via `pip`.

### **Format**
The file lists package names and optional version constraints. For example:
```plaintext
numpy==1.21.2
pandas>=1.3.0
matplotlib
```

### **Usage**
1. **Installing Dependencies**: Use `pip` to install packages listed in `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```
2. **Creating the File**: To generate a `requirements.txt` for your project:
   ```bash
   pip freeze > requirements.txt
   ```

### **Key Features**
- Focused on Python packages available on PyPI.
- Simple and widely supported for Python projects.
- Commonly used for deployments on platforms like Heroku, Docker, etc.

---

## 2. **Introduction to `environment.yml`**

`environment.yml` is a more versatile file format used to define Conda environments. It allows you to include Python packages, non-Python dependencies, and even specify channels.

### **Format**
A typical `environment.yml` file might look like this:
```yaml
name: my_environment
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.8
  - numpy=1.21.2
  - pandas>=1.3.0
  - matplotlib
  - pip:
      - some-python-package
```

### **Usage**
1. **Creating an Environment**: Use the `environment.yml` file to create a Conda environment called `environment_name`:
   ```bash
   conda env create -n environment_name -f environment.yml
   ```
   ```
   -n: flag for name; -f: flag for file 
   ```
2. **Updating an Environment**: Update an existing environment:
   ```bash
   conda env update -n environment_name -f environment.yml
   ```
3. **Exporting the Environment**: To generate an `environment.yml` from an existing Conda environment:
   ```bash
   conda env export > environment.yml
   ```

### **Key Features**
- Supports Python and non-Python dependencies (e.g., libraries, compilers).
- Allows specifying package channels (e.g., `conda-forge`).
- Ideal for managing complex cross-platform environments.

---

## 3. **Using the Environment with Jupyter**

Once you have created a Conda environment, you can use it with Jupyter by following these steps:

### **Install Jupyter in the Environment**
Ensure Jupyter is installed in the Conda environment:
```bash
conda install -c conda-forge notebook ipykernel
```

### **Add the Environment as a Jupyter Kernel**
Register the Conda environment as a Jupyter kernel:
```bash
python -m ipykernel install --user --name=your_environment_name --display-name "Python (your_environment_name)"
```
- Replace `your_environment_name` with the name of your Conda environment.
- The `--display-name` is how the environment will appear in Jupyter.

### **Start Jupyter Notebook**
Launch Jupyter Notebook from the terminal:
```bash
jupyter notebook
```

### **Select the Environment**
When creating a new notebook or running an existing one, select the environment from the kernel dropdown (e.g., "Python (your_environment_name)").

---

## 4. **Key Differences Between `requirements.txt` and `environment.yml`**

| **Aspect**               | **`requirements.txt`**               | **`environment.yml`**                      |
|--------------------------|--------------------------------------|--------------------------------------------|
| **Tool**                 | `pip`                               | `conda`                                    |
| **File Format**          | Plain text                          | YAML                                       |
| **Scope**                | Python packages from PyPI           | Python and non-Python dependencies         |
| **Channels/Repositories**| No channel support                  | Allows specifying Conda channels           |
| **Cross-Platform**       | Limited, Python only                | Better support for cross-platform setups   |
| **Usage**                | Simple Python environments          | Complex environments, including system tools |

---

## 5. **Using Both `requirements.txt` and `environment.yml`**

For projects requiring flexibility, you can use both files together:
1. Use `environment.yml` to manage the primary Conda environment, including non-Python dependencies.
2. Use `requirements.txt` for additional `pip` dependencies not available in Conda.

### Workflow Example:
1. **Create the Conda Environment**:
   ```bash
   conda env create -f environment.yml
   ```
2. **Install Additional Pip Packages**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Export Environment for Sharing**:
   ```bash
   conda env export > environment.yml
   ```

---

## 6. **Best Practices**

- **Use `environment.yml`** when working with Conda to leverage support for non-Python dependencies.
- **Use `requirements.txt`** when working with `pip` or deploying to platforms that rely on it.
- **Document Dependencies Clearly**: Include comments or documentation to explain why specific packages or versions are included.

---

## 7. **Common Commands**

### For `requirements.txt`
- Install dependencies:
  ```bash
  pip install -r requirements.txt
  ```
- Generate `requirements.txt`:
  ```bash
  pip freeze > requirements.txt
  ```

### For `environment.yml`
- Create a Conda environment:
  ```bash
  conda env create -f environment.yml
  ```
- Update an existing environment:
  ```bash
  conda env update -f environment.yml
  ```
- Export a Conda environment:
  ```bash
  conda env export > environment.yml
  ```

### For Jupyter
- Install Jupyter in the Conda environment:
  ```bash
  conda install -c conda-forge notebook ipykernel
  ```
- Add the environment as a Jupyter kernel:
  ```bash
  python -m ipykernel install --user --name=your_environment_name --display-name "Python (your_environment_name)"
  ```
- Start Jupyter Notebook:
  ```bash
  jupyter notebook
  ```

---

## 8. **Conclusion**

Choose the right file for your project:
- **Use `requirements.txt`** for simple Python projects with `pip`.
- **Use `environment.yml`** for complex projects requiring Conda's features.

For maximum flexibility, combine both tools to manage dependencies effectively.
