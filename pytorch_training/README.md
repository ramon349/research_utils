# Training .eval() and .train()
When training and validating your model, make sure to use model.train() in the training phase and model.eval() so that backpropagation is not happening during validation phase.
**note**, this is not the same as torch.no_grad() see [model.eval() vs torch.no_grad()](https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615)

# Datasets and Dataloaders
The **Dataset** class are a representation of your dataset where it will return the inputs (generally images) and labels (generally integer values of the labels but can be segmentation maps). You can customize the dataset as much as you want to do any fancy preprocessing or load more than just inputs like image IDs or secondary labels. The **Dataloader** class will generally apply shuffling, batching, and apply transforms to the dataset for easy data loading.

For customizing datasets and transforms see the pytorch tutorial: [Writing Custom Datasets, DataLoaders and Transforms](https://pytorch.org/tutorials/beginner/data_loading_tutorial.html)
