# Packaging a tool for Pypi

## Files required in your project

- See also [PyPA sample project](https://github.com/pypa/sampleproject)
- Tutorial [Packaging and Distributing Projects](https://packaging.python.org/distributing/)

### setup.py
- mandatory
- in root directory of project
- contains setup() function for installation

#### Arguments of the setup() function
keyword arguments
- name='project'   
The name which will be used to list your project on Pypi
- version='1.2.0'  
See versioning scheme  
Best is to have this duplicated in both setup.py and code itself
- description='description of my project'  
long_description=long_description  
long_description can be read from the README  
```python
with open(path.join(here, 'README.rst'), encoding='utf-8') as f:
    long_description = f.read()
```
displayed on PyPI together with project
- url="https://github.com/wdecoster/NanoPlot"  
Homepage url for project
- author="Wouter De Coster"
- author_email="decosterwouter@gmail.com"
- license='MIT'
- classifiers  
a list of classifiers to categorize project, such as
  - keywords='nanopore plotting quality control'
  - packages=find_packages()  
  packages which have to be included, can be explicitly listed or use setuptools.find_packages()
  - install_requires=[]  
  minimally required dependencies for project to run
  - package_data  
  listing additional files which need to be installed  
  uses relative paths
  - data_files  
  listing additional data files which have to be placed outside of the package  
  most often package_data suffices
  - scripts  
  keyword pointing to pre-made scripts to install, but not recommended method  
  instead use console_scripts in entry_points
  - entry_points containing console_script to register script interfaces (?)

### setup.cfg
ini file containing option defaults for setup.py

### Readme
- mandatory
- most commonly reStructuredText readme.rst

## <project> directory
- most common practice
- A directory with the same name as your package, containing your modules

### MANIFEST.in
- in certain cases
- for inclusion of additional files not automatically included by `setup.py sdist`