## 1. IP Spoofing simultaion carried out using [scapy](https://scapy.net/) and observed in [Wireshark](https://www.wireshark.org/)

### Open the terminal, Install scapy using pip
```
>>> pip install scapy
```


### Create a basic packet with src and destination IP address, ttl(time to live), protocol to be used etc.

```
>>> x = IP(ttl=64)
>>> x.src = "192.36.151.40"
>>> x.dst = "183.81.159.136"
>>> x = x/TCP()/"Test-Packet Recieved"
>>> x
<IP  frag=0 ttl=64 proto=tcp src=192.36.151.40 dst=183.81.159.136 |<TCP  |<Raw  load='Test-Packet Recieved'
```

### Open wireshark and connect to the same network to which sender is connected to. Open the Networkd and apply the filter as follows:
```
ip.dst == 183.81.159.136
```

### Press <b>Start capturing</b> button and then send the packets as below with ```count``` set to how many packets to be sent:
```
>>> send(x, count=10)
```
![Captured packets](wireshark_capture.png)

### You can add more information to the packet to mimic a real-world data.

## 2. Detection using Logistic Regression model
## Dataset:
### The dataset <b>DDoS SDN dataset</b> is downloaded from [kaggle](https://www.kaggle.com/datasets/aikenkazin/ddos-sdn-dataset).
### The dataset contains a total of 1,04,345 training examples.
### contains 3 categorial and 19 numerical features, a total of 22 features.
![Dataset preview](dataset_preview.jpg)

### contains a label column: ```0``` refers benign packet and ```1``` refers malignant IP packet.

## Model training:
### Install Required libraries using pip
```
pip install numpy pandas sklearn
```
### The data is pre-processed and split into training (0.75) and testing (0.25) using pandas and sklearn library respectively.

### The ```logisticRegression``` class in ```sklearn.linear_model``` is used to create an instance of the model. This model is trained with ```max_iters```(total no. of iterations to be run to train the model) is set to 10000.
## Model Evaluation:
### An accuracy of 70.16 % is achieved by using Logistic Regression. The accuracy can be further increased by the following:
- Using more no. of training examples
- Using more complex algorithms like Decision Trees, Random Forests, XGBoost etc.
- [Feature Engineering](https://towardsdatascience.com/what-is-feature-engineering-importance-tools-and-techniques-for-machine-learning-2080b0269f10), such that important features like src, dst, Protocol, pktrate, pktperflow etc. have more weights.