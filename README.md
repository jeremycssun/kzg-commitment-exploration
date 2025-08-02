# Readme

## Aim of this project

To explore different optimisation of KZG Commitment implementation in Python and reduce the run time of any of the 4 core elements.

* write up something

## Target to meet

1. Implement a KZG commitment scheme in Python
  * Completed implementation
  * Detailed documentation
  * Includes test cases with real data, and
  * Automated benchmarking.
    * Benchmark the KZG with an existing Merkle Tree commitment scheme
    * Benchmark all optimisation demonstrations

2. Optimises the performance
  * of more than two parameters
  * improve the algorithm significantly as a bonus

## How to read this notebook file

It is totally fine to read this notebook file in Github. Just note that the file was developed and designed to be run on Google Colab. Load this file in Google Colab for the best experience.

1. Download this file from the Github repository

2. Load the file up in:

* Google Colab with a Google account, an Internet connection and a browser, _or_

* Jupyter Notebook
  
## How to run this notebook file

1. **You do not have to run this Notebook**
    * Everything is already done for you, including the codes and the outputs.

2. **That said, if you want to play around with it, you may**
  * Load this file up in Google Colab or Jupyter Notebook with python 3.11 kernel extension. It should also work on other versions of python which is not tested.

    * <font color="red">Note:</font> The <code>py_ecc.bls12_381.pairing</code> module has a known issue with <code>Windows</code> -> <code>Python 3.11</code> and may lead to a kernel crash.

    * You also need the py_ecc library installed, or the ability to install this library if it is not available in your environment. It will not work in an environment as you do not have the administrator right to install python libraries.

3. **To Start**
    * Search for the string "Fast_Mode" and change it to 1
      * The optimisation demonstrations would now run a lot faster.
    * Search for the string "Tuning Variables"
      * It will bring you to the cell containing all configurable parameters.
      * Adjust them according to your needs
    * When you are done, press run all, or run the cell one at a time in order.
      * Note this may take a few minutes if not hours to run everything.
    * That is it.

>_Note: The default configuration uses a **3991-degree polynomial**, which causes the baseline (no optimization) showcase to take **~45 minutes**, and the entire notebook **~4 hours** to complete._

>_For quicker testing or debugging, set all polynomial degrees **below 100** to reduce the total runtime to **minutes**._

## Project Overview

### Component
> This notebook showcases a variety of KZG commitment implementations, performance benchmarks, and optimizations. It consists of the following components.

* Libraries Installation and Importing
  * Basic setup for required dependencies.

* Utilities Functions
  * Helper functions used throughout the notebook for commitments, timing, and verification.

* Global Variables
  * Real data and how they are converted into polynomials
  * Number of proofs, etc.


* KZG implementation
  * Our implementation, initially using the py_ecc.bls12_381 library
    * GitHub: [ethereum/py_ecc](https://github.com/ethereum/py_ecc)
  * Our implementation, switching over to the more advanced py_ecc.optimised_bls12_381
    * GitHub: [ethereum/py_ecc](https://github.com/ethereum/py_ecc)
  * A slight modification of kzg-python-toy
    * GitHub: [kassandraoftroy/kzg-python-toy](https://github.com/kassandraoftroy/kzg-python-toy)

* Includes a separate implementation of Merkle Trees to benchmark against KZG commitments.
  * *Note: Implemented in separate `.py` files (not part of this notebook).*

* Showcase Benchmarks
  
  * A. Compare 3 KZG Libraries
    * Setup time
    * Commitment time
    * Proof/Witness generation
    * Proof verification

  * B. Compare KZG and Merkle Tree
    * Commitment Time vs Input Size
    * Proving Time vs Input Size
    * Verification Time vs Input Size
    * In separated .py files, not in this file ATM

* Optimizations Benchmarks

  * Multi-point Batch Verification
    * Prove and Verify 25 points using batch techniques

  * Additive Homomorphism
    * Combine 8 commitments into 1 proof/verification using KZG's homomorphic properties

  * Trusted Setup (Trusted SRS)
    * Use pre-generated SRS up to degree 4095 (skip on-the-fly generation)

  * Combined Optimizations
    * Apply **all** optimizations for best performance

## Possible Improvements that were on our chart but left out at the end

- **Consistent Use of Tau and Evaluation Points (z)**  
  We could consider using the same τ and evaluation points z for all optimization tests. While this approach undermines the "discardable τ" philosophy — since it reuses trusted parameters — it improves consistency across benchmarks. This consistency can help us better isolate the performance impact of each optimization, making results easier to compare and interpret.

- **Pre-generated and Cached SRS**  
  Instead of regenerating the structured reference string (SRS) for each test, we could precompute it up to a high enough degree and cache it. This would reduce computational overhead during benchmarking. However, this approach assumes a shared τ, again conflicting with the discardable setup principle and reintroducing dependence on a common trusted setup.

- **Limitations of Batch Opening with Our SRS**  
  Our current trusted setup only includes powers of τ in G1 (i.e., [g^τ^i]) and does not produce the corresponding G2 elements (i.e., [h^τ^i]). As a result, some batch opening techniques — which require elements in G2 — are not compatible with our setup. Unless we modify our SRS to include G2 powers, we are limited in which batch optimizations we can apply.

## Acknowledgements & References

- **KZG Commitment Scheme**  
  *Constant-Size Commitments to Polynomials and Their Applications*  
  *Aniket Kate, Gregory M. Zaverucha, Ian Goldberg*  
  [Read the paper](https://iacr.org/archive/asiacrypt2010/6477178/6477178.pdf)

- **py_ecc** — Ethereum Foundation's elliptic curve library  
  [GitHub Repository](https://github.com/ethereum/py_ecc/)

- **kzg-python-toy** — A reference implementation by *Kassandra of Troy*  
  [GitHub Repository](https://github.com/kassandraoftroy/kzg-python-toy/)

- **Public Trusted SRS** — From the Ethereum KZG Ceremony  
  [ceremony.ethereum.org](https://ceremony.ethereum.org/#/record)

