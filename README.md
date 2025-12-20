# Neural Crypto System (NCS)

A deep learning-based encryption and decryption framework for secure end-to-end communication using adversarial neural networks.

## Overview

The Neural Crypto System (NCS) is an AI-powered cryptographic framework that learns encryption strategies through data-driven training rather than predefined mathematical rules. Unlike traditional cryptographic algorithms (AES, RSA), NCS uses deep neural networks to autonomously develop adaptive encryption mechanisms that evolve with data patterns and threat landscapes.

## Key Features

- **Autoencoder-Based Architecture**: Learns meaningful text representations for encryption/decryption
- **Key-Dependent Encryption**: Dynamic transformations using SHA-256 derived secret keys
- **Adversarial Training**: Joint training with attacker network (Eve) to strengthen security
- **High Security Metrics**: 
  - Bob (legitimate user) decryption: 99.67% accuracy
  - Eve (attacker) success rate: 17.66%
  - Security gap: 82.02%
  - Key sensitivity: 99.42%
- **Multi-Dataset Support**: Trained on diverse text datasets (IMDb, AG News, Yelp, SST-2, WikiText)
- **Scalable**: Handles variable-length text sequences up to 96 tokens

## System Architecture
```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐
│   Plaintext │ ───> │ Alice (Enc)  │ ───> │ Ciphertext  │
└─────────────┘      └──────────────┘      └─────────────┘
                            │                      │
                            │ Shared Key          │
                            ▼                      ▼
                     ┌──────────────┐      ┌─────────────┐
                     │ Bob (Dec)    │      │ Eve (Attack)│
                     └──────────────┘      └─────────────┘
                            │                      │
                            ▼                      ▼
                     ┌──────────────┐      ┌─────────────┐
                     │ Plaintext ✓  │      │ Gibberish ✗ │
                     └──────────────┘      └─────────────┘
```

### Core Components

1. **UltraSecureAutoencoder**: 512-dimensional embeddings with 6-layer encoder-decoder
2. **NuclearEncryption Layer**: Key-dependent transformations with multi-head gating
3. **EnhancedControlledEve**: 4-layer adversarial network simulating attacks
4. **Dynamic Key Generator**: SHA-256 based or random high-entropy key generation

## Installation
```bash
# Clone repository
git clone https://github.com/yourusername/neural-crypto-system.git
cd neural-crypto-system

# Install dependencies
pip install torch numpy matplotlib datasets
```

**Requirements:**
- Python ≥ 3.8
- PyTorch
- NumPy
- Matplotlib
- Hugging Face datasets library

## Quick Start
```python
from neural_crypto import NeuralCryptoSystem

# Initialize system
ncs = NeuralCryptoSystem()

# Encrypt message
plaintext = "This is a secret message"
key = ncs.generate_key()
ciphertext = ncs.encrypt(plaintext, key)

# Decrypt message
decrypted = ncs.decrypt(ciphertext, key)

print(f"Original: {plaintext}")
print(f"Decrypted: {decrypted}")
# Output: Original: This is a secret message
#         Decrypted: This is a secret message
```

## Training

The system uses two-phase training:

### Phase 1: Reconstruction Training
- **Goal**: Achieve >99% autoencoder reconstruction accuracy
- **Optimizer**: AdamW (lr=0.001)
- **Duration**: Until convergence (~100 epochs)

### Phase 2: Adversarial Encryption Training
- **Goal**: Bob >99% accuracy, Eve <15% accuracy
- **Optimizers**: 
  - Alice+Bob: AdamW (lr=0.001)
  - Eve: AdamW (lr=0.0002)
- **Duration**: ~100 epochs with dynamic encryption adjustment
```python
# Train model
ncs.train(
    dataset_name='imdb',
    phase1_epochs=100,
    phase2_epochs=100,
    batch_size=32
)
```

## Evaluation Metrics

| Metric | Value | Description |
|--------|-------|-------------|
| **Bob Similarity** | 99.67% | Legitimate decryption accuracy |
| **Eve Similarity** | 17.66% | Adversarial attack success rate |
| **Security Gap** | 82.02% | Bob - Eve accuracy difference |
| **Security Ratio** | 5.65× | Bob/Eve performance ratio |
| **Key Sensitivity** | 99.42% | Decryption failure with wrong keys |

## Model Evolution

The project evolved through 5 versions:

1. **v1 - Binary Encryption**: Basic feedforward networks (16-bit messages)
2. **v2 - Text-Based**: One-hot encoding with character-level encryption
3. **v3 - CycleGAN-Inspired**: Cycle-consistency and identity mapping
4. **v4 - DCGAN-Inspired**: Residual convolutional architecture with chaotic keys
5. **v5 - Proposed (DAA-NCS)**: Deep adversarial autoencoder with comprehensive evaluation

## Dataset Support

Trained and tested on:
- IMDb movie reviews
- AG News articles
- Yelp reviews
- SST-2 sentiment data
- WikiText corpus

Total: ~50,000 text samples with diverse linguistic patterns

## Results

The Deep Adversarial Autoencoder-Based Neural Cryptosystem (DAA-NCS) achieved:

- **Bob Similarity**: 99.67% ± 0.25% - Near-perfect legitimate decryption
- **Eve Similarity**: 17.66% ± 5.88% - Strong adversarial resistance
- **Security Gap**: 82.02% - Substantial separation between authorized and unauthorized access
- **Security Ratio**: 5.65× - Bob is nearly 6 times more accurate than Eve
- **Key Sensitivity**: 99.42% ± 0.50% - High resistance to wrong-key attacks

### Sample Decryption
```
Original:  "the movie was fantastic and thrilling"
Bob:       "the movie was fantastic and thrilling"  ✓
Eve:       "xhq m@vie w#s f@nt4stic 4nd thr!ll"     ✗
```

## Limitations

- **Slow Processing**: The model takes much longer to encrypt and decrypt messages compared to traditional methods like AES because it uses large neural networks
- **High Resource Usage**: Training requires powerful GPUs and takes several hours, making it difficult to run on regular laptops or mobile devices
- **Only Works for Text**: Currently, the system can only encrypt text messages, not images, videos, or other file types
- **Fixed Message Length**: Messages are limited to 96 characters, so longer texts need to be split into smaller chunks
- **No Mathematical Proof**: Unlike traditional encryption, we cannot mathematically prove how secure this system is - we can only test it experimentally
- **Training Instability**: Sometimes the model doesn't train properly and Eve becomes too strong or Bob becomes too weak, requiring us to restart training

## Future Work

- **Add Transformer Models**: Use attention-based architectures like BERT or GPT to better understand the context and meaning of longer messages during encryption

- **Support Multiple File Types**: Extend the system to encrypt not just text but also images, audio files, videos, and documents to make it more practical for real-world use

- **Reverse Engineering Analysis**: Study how attackers might try to reverse-engineer the neural network weights and encryption patterns to break the system, and develop defenses against such attacks

## Literature References

This work builds upon:

- **Abadi & Andersen (2016)**: "Learning to Protect Communications with Adversarial Neural Cryptography"
- **Li et al. (2021)**: "DeepEDN: A Deep Learning-Based Image Encryption and Decryption Network"
- **Kumar et al. (2025)**: "Deep Learning-Based Encryption Scheme Using DCGAN and Virtual Planet Domain"

## License

MIT License
