## Example Implementation of COLABFIT Portable ML Models

This repository contains example implementations of portable models that can utilize colabfit model driver. It will contain 3 models, 
- TorchScript implementation of pairwise model (Stillinger-Weber)
- Descriptor based ML model
- A Graph Neural Network

This shall highlight the difference between parameter file of different descriptor. The required parameter file is explained below,

1. Comments start with `#` and will be ignored. First entry in the file has to be number of elements in the model, followed by list of elements. Note no blank line or comment shall be present between number of elements and element list.
```
# Numbe rof elems
4
Si C Ni N

```

2. Following the above block should be a newline to mark completion of block. Next information required is the kind of preprocessing the ML model require. Current options include.
- None: model directly use the coordinated and neighbor information
- Descriptor: model uses descriptors of local environments
- Graph: model is a GNN and hence need the driver to first generate the graphs.
```
# Preprocessing
Descriptor

```
3. Influence distance
```
# Influence Distance
3.77118

```

4. Name of the TorchScript model file.
```
# Model name
model.pt

```

5. Whether model returns the scalar energy, or tuple containing energy and forces both. If False then driver will do a backprop pass through the model for forces.
```
# Return Forces
False

```

6. How many inputs does the model require. Example for descriptor it is usually 1, for Stillinger Weber it is 4 (coordinates, number of neighbors, neighbor list, contributing status)
```
# Number of Inputs
1

```

7. If model require descriptors, then name of descriptor needed
```
# Name of descriptor if any
SymmetryFunction
```