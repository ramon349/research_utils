# [Optuna](https://github.com/optuna/optuna)
```see the example notebook```

### RuntimeError: main thread is not in main loop
Sometimes when running optuna training, this error will occur and for me, it was because of matplotlib and plotting losses within the trials. So I just removed the part with the plotting in the code and it seems to run fine. See this [issue](https://github.com/r9y9/deepvoice3_pytorch/issues/5) for more context.

# [Optuna dashboard](https://github.com/optuna/optuna-dashboard)
Used to visualize the output optuna db. Quick use:
``` cd to the db location
optuna-dashboard sqlite:///yourdb.db
 ```
