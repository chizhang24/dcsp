# Divide-and-conquer state preparation

This repo contains the code used to generate the results for the publication 'A divide-and-conquer algorithm for quantum state preparation'.

arXiv link: https://arxiv.org/abs/2008.01511


If you happen to use this code please cite our paper:

Araujo, I., Park, D., Petruccione, F., da Silva, A.J. (2020). A divide-and-conquer algorithm for quantum state preparation

bibTex:
```
@article{araujo2020dcsp,
  title={A divide-and-conquer algorithm for quantum state preparation},
  author={Araujo, Israel F and Park, Daniel K and Petruccione, Francesco and da Silva, Adenilton J},
  journal={arXiv preprint arXiv:2008.01511},
  year={2020}
}
```
## Migration to Qiskit 1.x.x

### `random_vector.ipynb`
`Aer` is not available after `qiskit 1.0.0`. To use `Aer`, first install the namespace `qiskit-aer`

```python
%pip install qiskit-aer
```

To use `Aer.get_backend()`, in `qiskit 1.1.1`, we need to run 

```python
from qiskit_aer import Aer
```
before. 

And maybe `Aer` in `qiskit_aer` will be deprecated soon. 


`execute` cannot be used after `qiskit 1.0.0`. The following code in `random_vector.ipynb` 

```python
job = execute(circuit, backend_sim, shots = shots)
```

should be changed to 

```python
from qiskit import transpile
new_circuit = transpile(circuit, backend_sim)
job = backend_sim.run(new_circuit, shots = shots)
```
### `table1.ipynb`
All code works perfectly in `qiskit 1.1.1`, no need to do any change. 


### The `/QClassifier` folder 

The `/QClassifier` folder is very messed up. The `quantum_classifier.py` is the python script to get the results in Table 2 in the paper. 

There is a subfolder `/QClassifier/cin`, enclosing `/QClassifier/cin/dataset` and `/QClassifier/cin/pennylane`. `/QClassifier/cin/pennylane` is not the quantum computing library `pennylane`, nor are the python scripts under `/QClassifier/cin/pennylane` are part of the source code of `pennylane`. All the python scripts under the folder `/QClassifier/cin/` are user-defined. And this is the most confusing part of the source code. Keep in mind that all methods, functions and classes imported from `cin.*` are not part of the official python libraries `pennylane` and `scikit-learn`. The authors should have followed a clearer naming convention.

