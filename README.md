# Caffe_Tool_Csharp
A tool that support training with Caffe on Window

PREPARE 
1. Create "Data" folder that include "train" and "val" folder. Each of these folder contains sub folders for each class and images within it.
2. Creat "train.txt", "val.txt" in "Data" folder with each line include path for each image and the class for this image. Example: 0/123.jpg 0
3. Prepare "train_val.prototxt", "solver.prototxt", "deploy.prototxt", "synset.prototxt" in "Data" folder 
  - "train_val.prototxt": model for training
  - "solver.prototxt": for config hyperparameters
  - "deploy.prototxt": model for testing
  - "synset.txt" contain class map 
4. Build Caffe-window here https://github.com/BVLC/caffe/tree/windows with x64-Release mode. After that, there are some .exe files in Build/x64/release. The program will use executable files in this folder

RUN
1. Config software, Create "models" folder in "Data" folder
2. Run "CreateLMDB", "MakeMeanImage" and "Train" to training
  



The solver.prototxt is a configuration file used to tell caffe how you want the network trained.

## Parameters

#### base_lr  

This parameter indicates the base (beginning) learning rate of the network. The value is a real number (floating point).

#### lr_policy

This parameter indicates how the learning rate should change over time. This value is a quoted string.

Options include:

1. "step" - drop the learning rate in step sizes indicated by the **gamma** parameter.
1. "multistep" - drop the learning rate in step size indicated by the **gamma** at each specified **stepvalue**.
1. "fixed" - the learning rate does not change.
1. "exp" - **gamma**^_iter_
1. "poly" - the effective learning rate follows a polynomial decay, to be zero by the max_iter.  
**base_lr** * (1 - _iter_/**max_iter**) ^ (**power**)
1. "sigmoid" -  the effective learning rate follows a sigmod decay.  
**base_lr** * ( 1/(1 + exp(-**gamma** * (_iter_ - **stepsize**))))

where **base_lr**, **max_iter**, **gamma**, **step**, **stepvalue** and **power** are defined in the solver parameter protocol buffer, and _iter_ is the current iteration.

#### gamma

This parameter indicates how much the learning rate should change every time we reach the next "step." The value is a real number, and can be thought of as multiplying the current learning rate by said number to gain a new learning rate.

#### stepsize

This parameter indicates how often (at some iteration count) that we should move onto the next "step" of training. This value is a positive integer.

##### stepvalue

This parameter indicates one of potentially many iteration counts that we should move onto the next "step" of training. This value is a positive integer. There are often more than one of these parameters present, each one indicated the next step iteration.

#### max_iter

This parameter indicates when the network should stop training. The value is an integer indicate which iteration should be the last.

#### momentum

This parameter indicates how much of the previous weight will be retained in the new calculation. This value is a real fraction.

#### weight_decay

This parameter indicates the factor of (regularization) penalization of large weights. This value is a often a real fraction.

#### random_seed

A random seed used by the solver and the network (for example, in dropout layer).

#### solver_mode

This parameter indicates which mode will be used in solving the network.

Options include:

1. CPU
1. GPU

#### snapshot

This parameter indicates how often caffe should output a model and solverstate. This value is a positive integer.

#### snapshot_prefix

This parameter indicates how a snapshot output's model and solverstate's name should be prefixed. This value is a double quoted string.

#### net

This parameter indicates the location of the network to be trained (path to prototxt). This value is a double quoted string.

#### iter_size
Accumulate gradients across batches through the iter_size solver field. With this setting batch_size: 16 with iter_size: 1 and batch_size: 4 with iter_size: 4 are equivalent.

#### test_iter

This parameter indicates how many test iterations should occur per **test_interval**. This value is a positive integer.

#### test_interval

This parameter indicates how often the test phase of the network will be executed.

#### display

This parameter indicates how often caffe should output results to the screen. This value is a positive integer and specifies an iteration count.

#### type

This parameter indicates the back propagation algorithm used to train the network. This value is a quoted string.

Options include:

1. Stochastic Gradient Descent "SGD"
1. AdaDelta "AdaDelta"
1. Adaptive Gradient "AdaGrad"
1. Adam "Adam"
1. Nesterov’s Accelerated Gradient "Nesterov"
1. RMSprop "RMSProp"
