# Pytorch Vision
## Step by step command
1. download and build dataset
- download example dataset (SIGNS) from google drive [here](https://drive.google.com/file/d/1ufiR6hUKhXoAyiBNsySPkUwlvE_wfEHC/view)
- build SIGNS dataset: 
    - ```python build_dataset.py --data_dir data/SIGNS --output_dir data/64x64_SIGNS```
    - check build_dataset.py for dataset structure and format requirement
2. baseline model training
    - ```python train.py --data_dir data/64x64_SIGNS --model_dir experiments/base_model```
    - under experiments directory the base_model directory contain a file params.json, which sets the hyperparameters for the experiment.
3. hyperparameters search:
    - created a new directory learning_rate in experiments 
    - ```python search_hyperparams.py --data_dir data/64x64_SIGNS --parent_dir experiments/learning_rate```
4. Display the results of the hyperparameters search
    - ```python synthesize_results.py --parent_dir experiments/learning_rate```
5. Evaluation on the test set
    - ```python evaluate.py --data_dir data/64x64_SIGNS --model_dir experiments/base_model```
## TODO:
- [ ] build cifar10 dataset
- [ ] training on colab
## Reference
- [cs230 example code](https://github.com/cs230-stanford/cs230-code-examples)
Note: in folder `pytorch/vision`.
## Guidelines for more advanced use

We recommend reading through `train.py` to get a high-level overview of the training loop steps:
- loading the hyperparameters for the experiment (the `params.json`)
- loading the training and validation data
- creating the model, loss_fn and metrics
- training the model for a given number of epochs by calling `train_and_evaluate(...)`

You can then have a look at `data_loader.py` to understand:
- how jpg images are loaded and transformed to torch Tensors
- how the `data_iterator` creates a batch of data and labels and pads sentences

Once you get the high-level idea, depending on your dataset, you might want to modify
- `model/net.py` to change the neural network, loss function and metrics
- `model/data_loader.py` to suit the data loader to your specific needs
- `train.py` for changing the optimizer
- `train.py` and `evaluate.py` for some changes in the model or input require changes here

Once you get something working for your dataset, feel free to edit any part of the code to suit your own needs.
