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

# Documentation

## Dataset 
Base dataset: IDS 2018 

Following columns are the input to the model: 

'Protocol', 'Flow Duration', 'Tot Fwd Pkts', 'Tot Bwd Pkts', 'TotLen Fwd Pkts', 'TotLen Bwd Pkts', 'Fwd Pkt Len Max', 'Fwd Pkt Len Min', 'Fwd Pkt Len Mean', 'Fwd Pkt Len Std', 'Bwd Pkt Len Max', 'Bwd Pkt Len Min', 'Bwd Pkt Len Mean', 'Bwd Pkt Len Std', 'Flow IAT Mean', 'Flow IAT Std', 'Flow IAT Max', 'Flow IAT Min', 'Fwd IAT Tot', 'Fwd IAT Mean', 'Fwd IAT Std', 'Fwd IAT Max', 'Fwd IAT Min', 'Bwd IAT Tot', 'Bwd IAT Mean', 'Bwd IAT Std', 'Bwd IAT Max', 'Bwd IAT Min', 'Fwd PSH Flags', 'Bwd PSH Flags', 'Fwd URG Flags', 'Bwd URG Flags', 'Fwd Header Len', 'Bwd Header Len', 'Fwd Pkts/s', 'Bwd Pkts/s', 'Pkt Len Min', 'Pkt Len Max', 'Pkt Len Mean', 'Pkt Len Std', 'Pkt Len Var', 'FIN Flag Cnt', 'SYN Flag Cnt', 'RST Flag Cnt', 'PSH Flag Cnt', 'ACK Flag Cnt', 'URG Flag Cnt', 'CWE Flag Count', 'ECE Flag Cnt', 'Down/Up Ratio', 'Pkt Size Avg', 'Fwd Seg Size Avg', 'Bwd Seg Size Avg', 'Fwd Byts/b Avg', 'Fwd Pkts/b Avg', 'Fwd Blk Rate Avg', 'Bwd Byts/b Avg', 'Bwd Pkts/b Avg', 'Bwd Blk Rate Avg', 'Subflow Fwd Pkts', 'Subflow Fwd Byts', 'Subflow Bwd Pkts', 'Subflow Bwd Byts', 'Init Fwd Win Byts', 'Init Bwd Win Byts', 'Fwd Act Data Pkts', 'Fwd Seg Size Min', 'Active Mean', 'Active Std', 'Active Max', 'Active Min', 'Idle Mean', 'Idle Std', 'Idle Max', 'Idle Min' 

The different types of attack data are as follows ...

|Data |Size |
| :-: | :-: |
|Bot |286191 |
|DDOS attack-HOIC |686012 |
|DDoS attacks-LOIC-HTTP |576191 |
|DoS attacks-Hulk |461912 |
|DoS attacks-SlowHTTPTest |139890 |
|FTP-BruteForce |193354 |
|Infilteration |160739 |
|SSH-Bruteforce |187589 |
|Brute Force -Web |611 |
|Brute Force -XSS |230 |
|DDOS attack-LOIC-UDP |1730 |
|DoS attacks-GoldenEye |41508 |
|DoS attacks-Slowloris |10990 |
|SQL Injection |87 |
|Benign (Taken from the .csv file Divya mam provided) |2457307 |



All data is combined to a single dataframe and then is fit and scaled using Standard Scaler.  

### Selected Attacks (Size > 100000): 

- Bot 
- DDOS attack-HOIC 
- DDoS attacks-LOIC-HTTP 
- DoS attacks-Hulk 
- DoS attacks-SlowHTTPTest 
- FTP-BruteForce 
- Infilteration 
- SSH-Bruteforce 

### Not Selected Attacks: 

- Brute Force -Web 
- Brute Force -XSS 
- DDOS attack-LOIC-UDP 
- DoS attacks-GoldenEye 
- DoS attacks-Slowloris 
- SQL Injection 

### Various sets of dataframes are created: 

- attbenmix 
- selectedattackbenmix 
- notselectedattackbenmix 
- train\_loader 
- test\_loader 


### 1. attbenmix 

In this set of dataframes, each dataframe is a mix of one attack and some benign data. First 70% of available data of the attack and first 0.05% of the available benign data are mixed. Only 0.05% of benign data is used as benign data is of large size. 

<table><tr><th valign="top">Dataframe </th><th valign="top">Available data </th><th valign="top">Value Counts </th></tr>
<tr><td rowspan="2" valign="top">Bot.csv : (323198, 76) </td><td valign="top">Bot </td><td valign="top">200333 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">DDOS attack-HOIC.csv :(603073, 76) </td><td valign="top">DDOS attack-HOIC </td><td valign="top">480208 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">DDoS attacks-LOIC-HTTP.csv : (526198, 76) </td><td valign="top">DDoS attacks-LOIC-HTTP </td><td valign="top">403333 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">DoS attacks-Hulk.csv : (446203, 76) </td><td valign="top">DoS attacks-Hulk </td><td valign="top">323338 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top"><p>DoS attacks-SlowHTTPTest.csv : (220788, 76) </p></td><td valign="top">DoS attacks-SlowHTTPTest </td><td valign="top">97923 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">FTP-BruteForce.csv : (258212, 76) </td><td valign="top">FTP-BruteForce </td><td valign="top">135347 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">Infilteration.csv : (235382, 76) </td><td valign="top">Infiltration </td><td valign="top">112517 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
<tr><td rowspan="2" valign="top">SSH-Bruteforce.csv : (254177, 76)            </td><td valign="top">SSH-Bruteforce </td><td valign="top">131312 </td></tr>
<tr><td valign="top">Benign </td><td valign="top">122865 </td></tr>
</table>



### 2. selectedattackbenmix 

This dataframe contains all selected attacks and benign data in equal numbers. The last 100000 rows of all selected attack data and benign data are combined to create this dataframe. 

### 3. notselectedattackbenmix 

This dataframe contains all attack data that are not selected and benign data in equal numbers. The last 87 rows of all not selected attack data and benign data are combined to create this dataframe. Only 87 rows are selected, as in the set of not selected attack data, the attack data that has the least available data has only 87 rows. 

### 4. train\_loader 

In this set of dataframes, each dataframe contains the first 90% of one attack data. Only selected attack data is used. This set of dataframes is used to train the models. 

### 5. test\_loader 

In this set of dataframes, each dataframe contains the last 10% of one attack data. Only selected attack data is used. 






## <a name="_a5jidex4ybp1"></a>Auto-encoder Model
The autoencoder model implemented in the provided code is a deep autoencoder with a symmetric architecture for encoding and decoding. The architecture consists of fully connected (linear) layers with hyperbolic tangent (Tanh) activation functions. The purpose of the autoencoder is to perform dimensionality reduction and reconstruction of the input data. Here is a detailed description of the architecture:
### <a name="_5rn035jvkqz"></a>AEModel Class
- Parameters:
  - input\_dim: Dimensionality of the input data.
- Layers:
  - Fully connected layers (fc1 to fc9) with decreasing and then increasing dimensions.
  - Activation function: Hyperbolic Tangent (nn.Tanh()).
- Weight Initialization:
  - The initialization with Tanh activation is used to initialize the weights of each layer.
- Forward Method
  - The forward method performs the encoding and decoding operations through the fully connected layers with activation functions.
### <a name="_pov5y9f2e0m1"></a>Encoder Layers
- `fc1`: Fully connected layer with input size `input\_dim` and output size `input\_dim`. The output is passed through a Tanh activation function.
- `fc2`: Fully connected layer with input size `input\_dim` and output size 32. The output is passed through a Tanh activation function.
- `fc3`: Fully connected layer with input size 32 and output size 16. The output is passed through a Tanh activation function.
- `fc4`: Fully connected layer with input size 16 and output size 8. The output is passed through a Tanh activation function.
- `fc5`: Fully connected layer with input size 8 and output size 8. The output is passed through a Tanh activation function.
### <a name="_h37dkyz2e1d5"></a>Decoder Layers
- `fc6`: Fully connected layer with input size 8 and output size 16. The output is passed through a Tanh activation function.
- `fc7`: Fully connected layer with input size 16 and output size 32. The output is passed through a Tanh activation function.
- `fc8`: Fully connected layer with input size 32 and output size `input\_dim`. The output is passed through a Tanh activation function.
- `fc9`: Fully connected layer with input size `input\_dim` and output size `input\_dim`. The final output represents the reconstructed input.
### <a name="_w3i8hup5ri7h"></a>Activation Function
- Tanh activation function is used after each fully connected layer to introduce non-linearity and squash the output values between -1 and 1.
### <a name="_s3xelx24g0zt"></a>Weight Initialization
- He initialization with Tanh activation is used to initialize the weights of each layer. This helps in training deep networks by adjusting the initial weights based on the nonlinearity introduced by the Tanh activation.

In summary, the autoencoder model is designed to compress the input data into a lower-dimensional representation (encoding) and then reconstruct the original input from this representation. The encoder and decoder components are mirrored in terms of layer sizes, and the Tanh activation functions introduce non-linearity to the model. The model aims to learn a compact representation of the input data in the lower-dimensional space.
## <a name="_mrqaaxqjrlxv"></a>Federated Learning Framework
### <a name="_3a5m146u28a1"></a>Configuration Variables
- num\_clients: Number of clients in the federated learning setup.
- num\_selected: Number of clients selected for communication rounds.
- num\_rounds: Total number of communication rounds for global model training.
- epochs: Number of epochs for training each client model.
- server\_aggregate and server\_aggregate\_M: Functions for aggregating model weights received from clients using FedAvg and FedAvgM strategies.
### <a name="_7w9bb1dto312"></a>server\_aggregate Function
- Computes the average weight/bias across all clients using FedAvg strategy.
- Updates the global model with the averaged weights.
- Updates local models with the new global weights.
### <a name="_o040njqadrjm"></a>server\_aggregate\_M Function
- Computes the average weight/bias across all clients using FedAvgM strategy with momentum.
- Updates the global model with the averaged weights incorporating momentum.
- Updates local models with the new global weights.
### <a name="_m80nue2z5ps6"></a>client\_update Function
- Updates/trains the client model using local training data.
- Implements Mean Squared Error (MSE) loss for reconstruction.
- Returns the epoch loss.

### <a name="_w225quvwu4jx"></a>client\_syn Function
- Synchronizes the client model with the global model before training.
## <a name="_d91hgaaftbdu"></a>Usage
1. Create an instance of AEModel by providing the input\_dim.
1. Initialize configuration variables for federated learning.
1. Perform federated learning rounds using server\_aggregate or server\_aggregate\_M.
1. Update client models using client\_update on their respective local datasets.
1. Synchronize client models using client\_syn before each training round.

