# Uploading data to MD.ai
> Using MD.ai CLI: https://docs.md.ai/cli/installation/
1. make sure MDai is online/path is configured correctly
```python export PATH=$PATH:/home/jason/mdai ``` if that doesn't work, go to home dir and use:  ```"./mdai [commands]"```

2. make sure domain is correct:
```python ./mdai config domain mc.md.ai ```

3. make sure token is updated
```python ./mdai config token ### ```

4. make sure the correct project and dataset-id is being used
```python ./mdai project list-datasets --project-id project_id ```

5. upload from mayo servers to md.ai
```python ./mdai dataset load --dataset-id dataset_id data_location_in_server ```

# Making annotations in MD.ai
Make sure to create labels that are not metadata. Non-admin users will not be able to use your annotation labels if it's metadata. However, if you did make annotation labels as metadata, you can simply copy the annotations into a new annotation group and then people with non-admin access will be able to use those labels.

# Downloading annotations from MD.ai
see the example jupyter notebook: get_annotations.ipynb
