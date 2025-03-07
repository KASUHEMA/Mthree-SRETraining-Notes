# Python Installation and Printing Star Patterns

## 1. Creating a Virtual Environment:
```bash
python3 -m venv datastructure
```
**Explanation:** This creates a virtual environment called `datastructure`. A virtual environment is an isolated environment for Python projects where you can install dependencies without affecting your global Python installation.

**Purpose:** This helps manage project-specific dependencies and avoid conflicts with other projects.

## 2. Activating the Virtual Environment:
```bash
source datastructure/bin/activate
```
**Explanation:** Activates the `datastructure` virtual environment. Once activated, any Python or `pip` commands you run will use the environment's isolated setup.

**Purpose:** Ensures you're working in the virtual environment instead of your global Python environment.

## 3. Creating Directories for the Project:
```bash
mkdir -p src/basic_module/datastructure
```
**Explanation:** Creates a directory structure `src/basic_module/datastructure` for organizing your project files.

**Purpose:** Helps in organizing code, modules, and packages logically.

## 4. Creating a Python File (`pattern.py`) to Implement Logic:
```bash
cat > src/basic_module/datastructure/pattern.py << 'EOF'
def main():
    N = 9
    for i in range(0, N):
        for j in range(0, i):
            print(j, end=" ")
        print("")
    for i in range(0, N):
        for j in range(0, i):
            print(i, end=" ")
        print("")
    print()

if __name__ == "__main__":
    main()
EOF
```
**Explanation:** This writes a Python program into `pattern.py` that prints a specific pattern.
- The first loop prints numbers in increasing order.
- The second loop prints numbers in the same value repeatedly.
- The `main()` function is executed at the end.

**Purpose:** This is the core script of your project that will print patterns based on the loop logic.

## 5. Creating `__init__.py` Files:
```bash
touch src/basic_module/__init__.py
touch src/basic_module/datastructure/__init__.py
```
**Explanation:** Creates `__init__.py` files in both the `basic_module` and `datastructure` directories.

**Purpose:** These files turn the directories into Python packages, allowing for module imports.

## 6. Creating the `pyproject.toml` File:
```bash
cat > pyproject.toml << 'EOF'
[build-system]
requires = ["setuptools>=42", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "basic-module"
version = "0.1.0"
description = "A basic Python module"
readme = "README.md"
requires-python = ">=3.8"
dependencies = [
    "setuptools>=42",
    "wheel"
]
packages = ["basic_module", "basic_module.datastructure"]
EOF
```
**Explanation:** Defines metadata for your Python package.
- `[build-system]` section defines build requirements.
- `[project]` section contains metadata like the project name, version, dependencies, etc.

**Purpose:** The `pyproject.toml` file standardizes Python project metadata and build system configuration.

## 7. Creating a README File:
```bash
echo "# Basic Module" > README.md
```
**Explanation:** Creates a `README.md` file containing a description of your project.

**Purpose:** Provides documentation and information about the project.

## 8. Installing `pipx`:
```bash
apt install pipx
```
**Explanation:** Installs `pipx`, which allows running Python applications in isolated environments.

**Purpose:** Makes it easier to manage Python-based applications globally.

## 9. Installing the `build` Package:
```bash
pip install build
```
**Explanation:** Installs the `build` package, which helps in creating Python package distributions.

**Purpose:** Required to build the Python package from source.

## 10. Building the Wheel Distribution of Your Package:
```bash
python3 -m build --wheel
```
**Explanation:** Builds a wheel distribution of your package (`basic_module`).
- The `--wheel` option generates a `.whl` file (a packaged distribution of the module).

**Purpose:** Prepares your Python project for distribution.

## 11. Installing the Package Using `pipx`:
```bash
pipx install dist/basic_module-0.1.0-py3-none-any.whl
```
**Explanation:** Installs the built `.whl` file (`basic_module-0.1.0-py3-none-any.whl`) using `pipx`.

**Purpose:** Makes the package globally available.

## 12. Deactivating the Virtual Environment:
```bash
deactivate
```
**Explanation:** Deactivates the active virtual environment and returns to the system's global Python environment.

**Purpose:** It's a best practice to deactivate the virtual environment when you're done working in it.

---

## Conclusion
This guide covered the step-by-step process of:
1. Setting up a virtual environment and installing dependencies.
2. Creating a Python package directory structure and implementing a basic pattern printing script.
3. Defining project metadata and configuration using `pyproject.toml`.
4. Building a Python wheel distribution of the package.
5. Installing the package globally using `pipx`.
6. Deactivating the virtual environment after completing the setup.

This entire process ensures modularity, ease of distribution, and good development practices in Python programming. Following these steps helps manage dependencies effectively and maintain a clean development environment.

---
![image](https://github.com/user-attachments/assets/44d2a405-0f80-4470-9367-ffb790c966d6)

![image](https://github.com/user-attachments/assets/dce8fd88-12f4-488e-aa8d-0bdbdcc2a4d0)

![image](https://github.com/user-attachments/assets/2584c517-fff0-4a30-8c1e-a79aeff43a2c)

![image](https://github.com/user-attachments/assets/73ed465a-36aa-4cbe-8509-76382cf4211f)

![image](https://github.com/user-attachments/assets/220ff215-2572-4259-9fc8-a8247506dad8)

### Additional Activity
In breakout rooms, we revised Linux concepts and solved an LMS quiz to reinforce learning.
![image](https://github.com/user-attachments/assets/d2c29bc8-7ec8-41af-b02d-55ac8431f75a)

![image](https://github.com/user-attachments/assets/23d6678a-97a1-4d91-bde2-c6e0b7f9c049)

![image](https://github.com/user-attachments/assets/b1810bfd-86ad-4715-bec4-84972762c9aa)

![image](https://github.com/user-attachments/assets/124569f8-6173-4413-8225-79b97264cda3)


