# Uploading data to MD.ai
> Using MD.ai CLI: https://docs.md.ai/cli/installation/

0: make sure MDai is online/path is configured correctly
```python export PATH=$PATH:/home/jason/mdai ```
```if that doesn't work, go to home dir and use: "./mdai [commands]"```

1: make sure domain is correct:
```python ./mdai config domain mc.md.ai ```

2: make sure token is updated
```python ./mdai config token ### ```

3: make sure the correct project and dataset-id is being used
```python ./mdai project list-datasets --project-id project_id ```

4: upload from mayo servers to md.ai
```python ./mdai dataset load --dataset-id dataset_id data_location_in_server ```

# Downloading annotations from MD.ai
> see the example jupyter notebook: get_annotations.ipynb
