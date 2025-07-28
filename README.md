# kzg-commitment-exploration

The project start off as a group project on KZG commitment exploration. The main purpose is to look into KZG commitment and exploit any possible performance gain.

The project make use of the following libraries at the beginning and might span in other directions
* py_ecc.bls12_381               https://github.com/ethereum/py_ecc/
* py_ecc.optimised_bls12_381     https://github.com/ethereum/py_ecc/
* kassandraoftroy/kzg-python-toy https://github.com/kassandraoftroy/kzg-python-toy

This project should benchmark the following
1) Our kzg commitment implementation using ecc.bls12_381
2) Our kzg commitment implementation using ecc.optimised_bls12_381
3) A kzg commitment implementation using kzg-python-toy
4) Other possible solution

Each one branch off by
1) Batch verification (Additive Homomorphism: verify more than one data at a time.)
2) Using different chunk sizes

