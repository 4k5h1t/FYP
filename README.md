# FYP

## Introduction
To research and develop federated models, using the problem statement of Network Anomaly Detection. The base model used is an Autoencoder. 
An autoencoder is used to compress existing features and then trying to recreate them. The evaluation metric here is the recreation error.
When tackling a problem such as Network Anomaly Detection, essentially a classification problem, the confusion matrix and adjacent evaluation metrics are used.
We are using the IDS2018 network attack dataset.

## Phase 1
- [x] Research Network Anomaly Detection, Federated Learning, the IDS2018 dataset and Autoencoders.
- [x] Clean and pre-process the dataset based on relevant features identified through research. 
- [x] Create the base autoencoder model (binary - benign or malicious) for classification and test.
- [x] Set up constant documentation and version control systems in order to keep track of various experiments.
- [x] Try different methods of Federated Learning simulation (PyTorch, Tensorflow, scratch code).
- [x] Take the best in usability and move forward with research (Scratch coded simulation).
- [x] Implement the Federated Averaging algorithm.
- [x] Split dataset into separate files each containing one type of attack.
- [x] Assign the task of learning each of these files to one of the clients in the federated model.
- [x] Assess accuracy of each client separately (before federated averaging), on the attaqck it is trained for as well as on different attacks.
- [x] Perform Federated Averaging and assess accuracy again.
- [x] Create a separate test file containing mixed attack data and assess accuracy.
- [ ] Research Multiclass Autoencoders.
- [ ] Implement Multiclass Autoencoder at client level and assess effectiveness.
- [ ] Perform Federated averaging with implemented base multiclass autoencoder.
- [ ] Assess results and improve.

## Phase 2
- [ ] Research Machine Unlearning
- [ ] Implement Unlearning (wrongly train one client and attempt to unlearn)
- [ ] Assess results and improve. 

