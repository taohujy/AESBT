# AESBT
A deep Mixture-of-Experts (MoE) survival analysis framework , combining high-dimensional transcriptomic features with clinical covariates through a hybrid SVM–MLP gating mechanism. The model integrates WGCNA-derived pathway topology as a graph Laplacian regularizer to enforce biologically meaningful expert specialization.

## Core Architecture

### 1. Shared Encoder
A single fully-connected layer with  activation and dropout . Projects high-dimensional gene expression into a shared latent space consumed by all expert networks.

### 2. Expert Cox Networks
Each expert reuses the shared encoder and appends MLP branch  that outputs the partial hazard. Experts are trained independently on bootstrap subsamples with three objectives combined at every step.

### 3. Posterior Likelihood Expert Assignment
After expert pretraining, each training sample is softly assigned to experts based on the partial likelihood under each expert's risk function.

### 4. Hybrid Gating Network
An MLP that takes a patient's standardized age concatenated with SVM posterior probabilities over the classes, and outputs softmax weights over the experts.

## Installation

pip install torch pandas numpy scikit-learn networkx
pip install pycox sksurv
pip install PyWGCNA
 
