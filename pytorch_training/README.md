# Training .eval() and .train()
When training and validating your model, make sure to use model.train() in the training phase and model.eval() so that backpropagation is not happening during validation phase.
**note**, this is not the same as torch.no_grad() see [model.eval() vs torch.no_grad()](https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615)

# Datasets and Dataloaders
The **Dataset** class are a representation of your dataset where it will return the inputs (generally images) and labels (generally integer values of the labels but can be segmentation maps). You can customize the dataset as much as you want to do any fancy preprocessing or load more than just inputs like image IDs or secondary labels. The **Dataloader** class will generally apply shuffling, batching, and apply transforms to the dataset for easy data loading.

For customizing datasets and transforms see the pytorch tutorial: [Writing Custom Datasets, DataLoaders and Transforms](https://pytorch.org/tutorials/beginner/data_loading_tutorial.html)

# Transforms
For imaging datasets, you'll generally have transforms of this form:

```python
transforms = {
    'train': transforms.Compose([
        transforms.RandomResizedCrop(224),
        transforms.RandomHorizontalFlip(),
        transforms.ToTensor(),
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
    ]),
    'val': transforms.Compose([
        transforms.Resize(256),
        transforms.CenterCrop(224),
        transforms.ToTensor(),
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
    ]),
}
```

One can see that the train dataloder has various random transforms (RandomResizedCrop and RandomHorizontalFlip). This is to augment the dataset with transforms so that the model can see more varieties of the dataset. However, the validation doesn't have any random transforms because that's how the data will be given to the model in testing/inference. 

**Generally** .ToTensor() and .Normalize() will always be the final two transforms applied as pytorch transform usually works will PIL images and need to be converted to tensors and normalized. The normalization values: *mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]* are normalization values for imageNet pre-trained images. However, in practice, using *mean=0.5 and std=0.5* is more common.
