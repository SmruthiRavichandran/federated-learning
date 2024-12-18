
# A PyTorch framework for federated learning

**What is federated Learning?**

Federated learning is a machine learning approach where models are trained across multiple decentralized devices or servers holding local data samples, without transferring the data to a central server. This ensures data privacy and security by keeping sensitive information on local devices. The system aggregates locally computed model updates to improve a global model. It is commonly used in applications like personalized recommendations, healthcare, and finance. Federated learning addresses challenges like data heterogeneity, communication efficiency, and privacy concerns.

Here the federated Learning is combined with CNN model and LSTM with CharLSTM model uses an LSTM to model sequential data and learn dependencies between characters.
Character-Level Language Model: This model can predict the next character in a sequence based on previous characters.


---
## Index
1. [Install requirements](#install-requirements)
2. [Catalog](#catalog)
3. [Training](#training)
4. [Options](#options)

---

## [Install requirements](#index)

To install requirements, run the command below:

```bash
pip install -r requirements.txt
```

## [Catalog](#index)
1. [Datasets](#datasets)
2. [Models](#models)
3. [Federated learning strategies](#federated-learning-strategies)

### Datasets

- [x] MNIST: 10-digit dataset.
- [x] Fashion-MNIST: clothing dataset with 10 classes.
- [x] CIFAR-10, CIFAR-100: image dataset with 10 and 100 classes, respectively.
- [x] FEMNIST: large version of MNIST for federated learning benchmarking.
This project contains a small version of FEMNIST with 520 clients.

### Models

- [x] Simple CNN models: used in various FL papers.
- [x] ResNets: ResNet18, ResNet34, ResNet50, ResNet101, ResNet152 are supported.

### Federated learning strategies

- [x] FedAvg: Communication-Efficient Learning of Deep Networks from Decentralized Data [[`arXiv`](https://arxiv.org/abs/1602.05629)]
- [x] SCAFFOLD: Stochastic Controlled Averaging for Federated Learning [[`arXiv`](https://arxiv.org/abs/1910.06378)]
- [x] FedDyn: Federated Learning Based on Dynamic Regularization [[`arXiv`](https://arxiv.org/abs/2111.04263)]

## [Training](#index)

For all tasks for FedDyn, it is good to keep `alpha` as 1.0, which is a default value.

1. [MNIST](#mnist)
2. [Fashion-MNIST](#fashion-mnist)
3. [FEMNIST](#femnist)
4. [CIFAR-10, CIFAR-100](#cifar-10-cifar-100)

### MNIST

- Participation ratio: 0.1, IID distribution
```bash
python main.py --dataset mnist --iid --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, 2-shards-per-client distribution
```bash
python main.py --dataset mnist --spc --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset mnist --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

- Participation ratio: 1.0, IID distribution
```bash
python main.py --dataset mnist --iid --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, 2-shards-per-client distribution
```bash
python main.py --dataset mnist --spc --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset mnist --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

### Fashion-MNIST

- Participation ratio: 0.1, IID distribution
```bash
python main.py --dataset fashion-mnist --iid --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, 2-shards-per-client distribution
```bash
python main.py --dataset fashion-mnist --spc --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset fashion-mnist --model cnn --frac 0.1 --epochs 300 --lr 0.01 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

- Participation ratio: 1.0, IID distribution
```bash
python main.py --dataset fashion-mnist --iid --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, 2-shards-per-client distribution
```bash
python main.py --dataset fashion-mnist --spc --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset fashion-mnist --model cnn --frac 1.0 --epochs 300 --lr 0.01 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

### FEMNIST

Keep in mind that FEMNIST is naturally non-IID and setting `iid` as true will only make an error.

- Participation ratio: 0.1
```bash
python main.py --dataset femnist --model cnn --frac 0.1 --epochs 500 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0
```bash
python main.py --dataset femnist --model cnn --frac 1.0 --epochs 500 --lr 0.01 --n_clients 100 --fed_strategy fedavg
```

### CIFAR-10, CIFAR-100

A CNN model can be insufficient to train CIFAR-100, so consider using ResNet50.

- Participation ratio: 0.1, IID distribution
```bash
python main.py --dataset cifar10 --iid --model cnn --frac 0.1 --epochs 1000 --lr 0.02 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, 2-shards-per-client distribution
```bash
python main.py --dataset cifar10 --spc --model cnn --frac 0.1 --epochs 1000 --lr 0.02 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 0.1, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset cifar10 --model cnn --frac 0.1 --epochs 1000 --lr 0.02 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

- Participation ratio: 1.0, IID distribution
```bash
python main.py --dataset cifar10 --iid --model cnn --frac 1.0 --epochs 1000 --lr 0.02 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, 2-shards-per-client distribution
```bash
python main.py --dataset cifar10 --spc --model cnn --frac 1.0 --epochs 1000 --lr 0.02 --n_clients 100 --fed_strategy fedavg
```

- Participation ratio: 1.0, Dirichlet distribution (beta: 0.3)
```bash
python main.py --dataset cifar10 --model cnn --frac 1.0 --epochs 1000 --lr 0.02 --n_clients 100 --beta 0.3 --fed_strategy fedavg
```

## [Options](#index)
1. [Federated learning arguments](#federated-learning-arguments)
1. [Model and dataset arguments](#model-and-dataset-arguments)
1. [Optimizing arguments](#optimizing-arguments)
1. [Misc](#misc)

### Federated learning arguments
- epochs (default=300): total rounds of federated learning training
- n_clients (default=100): number of clients participating in federated learning
- frac (default=0.1): fraction of clients participating in each round. 1.0 for full participation
- local_ep (default=5): number of local epochs for each client
- local_bs (default=100): local batch size
- test_bs (default=128): test batch size
- lr (default=0.01): learning rate
- lr_decay (default=0.9): learning rate decay
- lr_decay_step_size (default=500): step size to decay learning rate

### Model and dataset arguments
- model (default='cnn'): model used for training (options: 'mlp', 'cnn', 'resnet18', 'resnet34', 'resnet50', 'resnet101', 'resnet152')
- dataset (default='mnist'): name of dataset (options: 'mnist', 'fashion-mnist', 'femnist', 'cifar10', 'cifar100')
- iid (action='store_true'): whether i.i.d or notc (default: non-iid)
- spc (action='store_true'): whether spc or not (default: Dirichlet distribution)
- beta (default=0.2): beta for Dirichlet distribution
- n_classes (default=10): number of classes. Automatically modified in code
- n_channels (default=1): number of channels. Automatically modified in code

### Optimizing arguments
- optimizer (default='sgd'): Optimizer (options: 'sgd', 'adam')
- momentum (default=0.0): SGD momentum
- fed_strategy (default='fedavg'): optimization scheme (options: 'fedavg', 'scaffold', 'feddyn')
- alpha (default=1.0): alpha for feddyn

### Misc
- n_gpu (default=4): number of GPUs to use
- n_procs (default=1): number of processes per processor
- seed (default=0): random seed
- no_record (action='store_true'): whether to record or not (default: record)
- load_checkpoint (action='store_true'): whether to load model (default: do not load)
- no_checkpoint (action='store_true'): whether to save best model (default: checkpoint)

### For the specific settings:

Namespace(epochs=300, n_clients=100, frac0.1, local_ep=5, local_bs=100, test_bs=128, 1r=0.01, lr_decay=0.9, lr_decay_step_size=500, model=scnn', dataset='mnist', iid=False, spc=False, beta=0.2, n_classes=10, n_channels=1, timizer=ssgds, momentuffw0.0, fed_strategy=sfedavgs, alpha=1 .0, n_gpu=4, n_procs=1, seed=0, no_record=False, load_checkpoint=False, no_checkpoint=False), the resulst are shownn as a graph

![graph results of federated learing](https://github.com/user-attachments/assets/adffe4b0-dc64-4ea8-b75c-7982d4034bfe)



