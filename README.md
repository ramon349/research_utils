# research_utils
Common commands and utils to take note of when working in lab.

Feel free to add to the README or add scripts that makes life easier here.

./pytorch_training: contains common pytorch training tips, tricks, and mistakes (dataloading, transforms, modes, etc.)

# envrionment files
### ncsnv2.yml
> Environment.yml file for "Improved Techniques for Training Score-Based Generative Models." https://github.com/ermongroup/ncsnv2
### SAM.yml
> Environment.yml file for "Segment Anything" [https://github.com/ermongroup/ncsnv2](https://github.com/facebookresearch/segment-anything)

# Using Jupyter Notebook on server (MobaXTerm)
First set up an SSH tunnel with the following parameters (with your credentials):
![SSH Tunnel setup](images/port_forwarding_servers.png)
Then start the SSH tunnel, bash and then run the following command:
```python
jupyter notebook --no-browser
```

# Tmux (running processes in the server without disconnecting)
```python
# create a new session with a session name (easier to figure out which session is which)
tmux new -s session_name

#Detaching from Tmux Session:
Ctrl+b d

#Listing current tmux sessions:
tumx ls

#Attaching to tmux sessions:
tmux attach-session -t named_session

#Killing sessions:
tmux kill-session -t 3

# scrolling through errors in copy mode:
Ctrl+b,[
```

# Cleaning up disk space:
### check disk space to a directory:
```python
du -sh directory_name
```
### remove directory recursively:
```python
rm -r directory_name
```

# Copying to and from different servers
Use rsync: ```python rsync -r username@server1_IP:source_dir username@server2_IP:destination_dir ```

# Copying to and from  GCP
1. bash (to use gcloud)
2. Auth login first using:
```python gcloud auth login --no-launch-browser ```
3. Use gsutil to copy from one dir to another in the server:
```python gsutil -m cp -r "gs://ml-bf1c-phi-shared-aif-us-p/GCP_location" /media/Datacenter_storage/server_location/ ```

# Memory issues:
### Memory not being released (cuda running out of memory error)
> if you train a model and it runs for a few loops (batches or epochs) but then suddenly runs out of memory, the issue is probably that some variable is compounding and its memory is not being released. A few things you can do to debug is:
0) check memory usage after each loop using torch.cuda.memory_allocated()
```python
# this code will print device memory usage in MB, i being batch or epoch number
print('batch {}: {:.2f}MB'.format(i, float(torch.cuda.memory_allocated(device=DEV) / (1024 * 1024))))
```

1) collect garbage and release cache ([https://docs.python.org/3/library/gc.html](https://stackoverflow.com/questions/59129812/how-to-avoid-cuda-out-of-memory-in-pytorch))
```python
import gc
import torch

gc.collect()
torch.cuda.empty_cache()
```
2) zero grad the optimizers - PyTorch accumulates the gradients on subsequent backward passes and if you don't the gradient would be a combination of the old gradient, which you have already used to update your model parameters and the newly-computed gradient. (https://stackoverflow.com/questions/48001598/why-do-we-need-to-call-zero-grad-in-pytorch)
```python
optimizer.zero_grad(set_to_none=True)
```
3) make sure to add .items() not tensors in history or anything that will be evaluated at the end of the loop
```python
# if loss is a tensor and used in gradient calculations then loss_sum will accumulate memory
loss = loss_fn(x, y)
loss_sum += loss
# print(loss) will give something like: "tensor(0.3652, device='cuda:0', grad_fn=<MulBackward0>)"

# the .item() of the tensor will just give the value and remove any gradient 
loss = loss_fn(x, y)
loss_sum += loss.item()
# print(loss.item()) will give something like: "0.3651849031448364"
```

### pip running out of memory (can't install because of OS memory)
> this might occur if you have a new conda environment and trying to install a separate pip and packages on it
if so, try conda clean (Remove unused packages and caches.): https://docs.conda.io/projects/conda/en/latest/commands/clean.html
```python
conda clean -a
```

# Random Errors and quality of life stuff
### RuntimeError: main thread is not in main loop
Sometimes when running optuna training, this error will occur and for me, it was because of matplotlib and plotting losses within the trials. See this [issue](https://github.com/r9y9/deepvoice3_pytorch/issues/5) for more context. So you can either remove the plotting during optuna training or use the following lines:

```python
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
```

### Plus Minus sign (±)
```python
print('\u00B1')  # will give you the ±
```

# Git issues:
### commited large files to git repo and need to remove (blob.txt as an example):
> Github won't let you push large files to your repo and if you somehow got to the limit and wanted to push something small that would put it over the limit, it will cause issues. However, since Github keeps the history of your commits with the files, the solution is not as simple as removing the large files from your repo. So you'll need to delete the large files from your repo history through BFG Repo-Cleaner. (There are other ways to remove from the history but for me, it was the easiest and most straight forward method).

Use BFG Repo-Cleaner: https://rtyley.github.io/bfg-repo-cleaner/
3
