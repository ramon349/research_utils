# Why are we using UV 
- trying out some quick replacements for conda given the licence issues 
- allows you to install specific python version and doesn't depend on the current system python 

# What is UV 
- it is a  python package and project manager 
- allows you to install packages using  uv pip install the normal way you'd use use pip 
- the main interest is kk

# Project Manager Vs package Managers 

# Before you start 
- in your ~/.bashrc set an enviroment variable for your uv_cache_dir 
- this is essential or else your home directory will become bloated quickly.
```bash 
export UV_CACHE_DIR="PATH_TO_A_FOLDER_IN_DATACENTER"
```

# Starting a project 
- we asume your project is structured as follows 
- set up your directory so you have the directories in the second level i.e  project_code,notebooks,data
- uv will generate the files inside proect code later 
```
project_folder
    notebooks\
    data\
    project_code\
        .venv
        pyproject.toml
        uv.lock
``` 
- cd to inside project_code 
- run  ```bash  uv init venv --python 3.11 ```
- run  ```bash  uv init ``` will create the project files 
- i've created an example pyproject toml. This one is essential because we must be certain of which cuda runtime we are using for some projects 

# Adding other files 
- it is recommended you use uv add packageName isntead of uv pip 
- since it will update the toml file accordinly and apply the checks for versions and avoid unecessary udpates  

# TODO 
- make the pyproject.toml a basic pytorch with cuda. 
- add the options of cuda11 or cuda12 
- add instructions for someone to make an env using this reference toml 