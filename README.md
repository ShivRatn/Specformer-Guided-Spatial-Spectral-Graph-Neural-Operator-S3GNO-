Project: Spectral-Spatial GNNs for Structural Blast Load Prediction
Overview
This project provides and compares three distinct Graph Neural Network (GNN) architectures designed to predict the dynamic blast load time-series (p(t)) at every node of a box-girder structural system.   

The core challenge is modeling a phenomenon that is simultaneously local (fine-grained stress) and global (coherent shockwave propagation). Conventional GNNs are ill-suited for this, as they are either limited to local message-passing or suffer from "over-smoothing" when made deep enough to capture long-range effects.   

Core Methodology: PCA Compression
To make this high-dimensional problem computationally tractable, all three models share a crucial preprocessing step. The (N×T) time-series data is compressed using Principal Component Analysis (PCA) into a compact 20-dimensional latent representation (Φ∈R 
N×20
 ). This reframes the learning task from spatio-temporal prediction to a spatial regression problem: the GNNs must learn to predict these 20 static coefficients for each node.   

Model Architectures
PCA-GNN (Baseline): A hybrid model that first applies PCA and then uses a standard Graph Attention Network (GAT) to learn spatial dependencies. Its architecture is limited to local neighborhood aggregation, which fails to capture the global physics. This is "clearly" demonstrated by its catastrophic 193.97% error in predicting the total impulse (energy).   

Sp2GNO (Spatio-Spectral Graph Neural Operator): A more advanced dual-path baseline that processes information in parallel: a local spatial path for fine-grained details and a global spectral path (using the fixed graph Laplacian) to model long-range dependencies.   

S3GNO (Specformer-Guided Spectral-Spatial GNO): The novel proposed architecture. It introduces a transformer-based "Specformer" module that learns the graph's eigenvalue correlations. It uses this to reconstruct an adaptive adjacency matrix, dynamically capturing frequency-dependent connectivity. This adaptive graph is then used in a dual-path operator. This "self-attentive spectral adaptation" allows S3GNO to "clearly outperform" the other models, achieving a 0.9522 R 
2
  and the lowest error on all metrics.
