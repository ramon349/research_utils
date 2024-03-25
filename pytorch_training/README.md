# Training .eval() and .train()
When training and validating your model, make sure to use model.train() in the training phase and model.eval() so that backpropagation is not happening during validation phase.
*note, this is not the same as torch.no_grad() see [model.eval() vs torch.no_grad()] (https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615)
