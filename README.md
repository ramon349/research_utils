# research_utils
Common commands and utils to take note of when working in lab.

Feel free to add to the README or add scripts that makes life easier here.

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
```

# Git issues:
### commited large files to git repo and need to remove (blob.txt as an example):
Use BFG Repo-Cleaner: https://rtyley.github.io/bfg-repo-cleaner/
