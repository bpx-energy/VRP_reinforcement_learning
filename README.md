# VRP_reinforcement_learning
We use Reinforcement for solving Travelling Salesman Problem (TSP) and Vehicle Routing Problem (VRP).

We present an end-to-end framework for solving the Vehicle Routing Problem (VRP) using reinforcement learning. In this approach, we train a single model that finds near-optimal solutions for problem instances sampled from a given distribution, only by observing the reward signals and following feasibility rules. Our model represents a parameterized stochastic policy, and by applying a policy gradient algorithm to optimize its parameters, the trained model produces the solution as a sequence of consecutive actions in real time, without the need to re-train for every new problem instance. On capacitated VRP, our approach outperforms classical heuristics and Google's OR-Tools on medium-sized instances in solution quality with comparable computation time (after training). We demonstrate how our approach can handle problems with split delivery and explore the effect of such deliveries on the solution quality. Our proposed framework can be applied to other variants of the VRP such as the stochastic VRP, and has the potential to be applied more generally to combinatorial optimization problems.


Dependencies:
- Numpy
- Tensorflow>= 1.2
- tqdm

How to run:

By default the code is running in the training mode on a single GPU. For running the code, you can use the following command

> python main.py --task=vrp10

It is also possible to add other config params (example):

> python main.py --task=vrp10 --gpu=0 --n_glimpses=1 --use_tanh=false

I have included a list of all configs in the > config.py file. Also task specific parameters are available in > task_specific_params.py

Inference:

For running the trained model for inference, it is possible to turn off the training mode. For this, you need to specify the directory of the trained model, otherwise random model will be used for decoding:

> python main.py --task=vrp10 --is_train=False --model_dir=./path_to_your_saved_checkpoint

The default inference is run in batch mode, meaning that all testing instances are fed simultanously. It is also possible to do inference in single mode, which means that we decode instances one-by-one. The latter case is used for reporting the runtimes and it will display detailed reports. For running the inference with single mode, you can try:

> python main.py --task=vrp10 --is_train=False --infer_type=single --model_dir=./path_to_your_saved_checkpoint

