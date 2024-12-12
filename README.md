# RIC-assisted-realtime-video-QoE-prediction-system
## Introduction 
_Y. Sun, W. Xiong, G. Pan,S. Xu, S. Zhang and X. Chen.QoE Prediction in RIC-assisted Wireless Real-time Video Transmission System with Transformer, Submitted to IEEE Transactions on Vehicular Technology._

This is the Github repository which provides a detailed introduction to the experimental environment and data acquisition process of this letter. The main aim of the repository is to present our RIC-assisted realtime video QoE prediction system, discuss and report issues. This demo showcases the architecture of the system and the process of obtaining data. All the experiments mentioned in the letter are based on the datasets collected on the prototype platform. 
## Experimental environment
Our proposed prediction scheme has been tested on our prototype communication platform based on OpenAirInterface (OAI) and a real-time video transmission platform based on Web Real-Time Communication (WebRTC). The communication platform consists of a software-defined Evolved Packet Core (EPC) and Radio Access Network (RAN), a RIC platform, a Radio Frequency Front-end (USRP) B210, and commercial User Equipment (UE). The real-time video transmission platform is composed of a server and client side, as illustrated in the figure below.

The system can interconnect with commercial User Equipment (UE) and provide them with a cellular network for data transmission. The UE receives video sent by the video server and obtains Quality of Experience (QoE) related information from the server. Concurrently, it can acquire bandwidth-related Radio Access Network (RAN) information from the RAN side through the RAN intelligent controller(RIC) server and generate datasets.

<div align="center">
  
  <img src="https://github.com/alen-quan/RIC-assisted-realtime-video-QoE-prediction-system/blob/main/Fig 1. Experimental Environment.jpg" width ="700" alt="Environment">
  <p align="center">Fig. 1. The snapshot of the RIC-assisted wireless communication system.</p>
  
   </div>

The details of hardware and software configurations are listed in the following table.
  <p align="center">Table I   Configurations of OAI-based Prototype Platform.</p>
  
   </div>
  
  <div align="center">
  
  Component |Hardware|Software|
  ----|----|----|
  RAN/eNB|Intel i7-8559U|OpenAirInterface (OAI)|
  EPC|Intel i7-8559U|Openair-cn|
  RIC|Intel i9-9980HK|Edgegallery|
  WebRTC server|Intel i9-9980HK|WebRTC|
  Radio Frequency Front-End|Ettus USRP B210|N/A|
  UEs|6×Huawei Nexus 6P|Android 8.0|
  
  </div>
  
## Data Collection
  We collect datasets under  different transmission conditions based on the RIC-assisted realtime-video QoE prediction system.Specifically, we change the state of the wireless network through the movement of ue in the region.
### Process 

To generate datasets for different wireless environments, we have done the following implementation work. 
  * Firstly, we open the OAI system, including eNB and EPC (three core network elements, i.e., MME, HSS and SPGW). 
  * Secondly, we switch the commercial UEs from airplane mode to non-airplane mode. The UEs are connected to the cellular network as shown in the figure below.
  * Thirdly, The UE receives and plays real-time video from the WebRTC server, and the video bitrate is automatically selected according to the network status.
  * Fourthly, the RIC server collects the RAN information through the flexRAN feedback during the $t$-th transmission period and saves them to the dataset according to a certain format. And WebRTC server records real-time video QOE-related information and generates datasets to send to the RIC. The details of RAN information are listed in the following table.
 <div align="center">
  
   <img src="https://github.com/alen-quan/RIC-assisted-realtime-video-QoE-prediction-system/blob/main/Fig 2. UE connected to cellular network illustration.png"  width ="400"  alt="illustration">
  
   </div>
   
   <p align="center">Fig. 2. The snapshoot of UE connected to cellular network illustration.</p>

The data set collected in the above steps will be trained and tested on the RIC. 

The data training process is performed on the RIC using the Pytorch platform. When the offline training process is complete, the video stream QoE prediction model is hosted on the RIC. The proposed prediction scheme and baseline prediction scheme obtain the RAN context measurement results and video QoE information of the previous $t_h$ = 6 transmission cycles, and predict the video stream QoE of the next transmission cycle.

## Experimental Result

In Figure 3 and Table 3, we have shown the comparison between the predicted results of the proposed scheme and the real values, as well as the performance comparison with the baseline algorithm.As shown in Table 3, the Transformer based prediction algorithm proposed in this paper has better MAE than the baseline algorithm under the three QoE defined indicators, and tt also performed well in the E<sub>50</sub> and E<sub>90</sub>.
<div align="center">
  
<img src="https://github.com/alen-quan/RIC-assisted-realtime-video-QoE-prediction-system/blob/main/Fig 3. The predicted QoE value versus the ground-truth QoE value.png"  width ="600" alt="Fig. 3. The predicted QoE value versus the ground-turth QoE value">

 </div>
<p align="center">Fig. 3. The predicted QoE value versus the ground-turth QoE value.</p>
  <p align="center">Table III   Performance Comparison among Different Prediction Algorithms</p>

<div align="center">
  
### Performance Analysis of Different Algorithms

| **Method**       | **QoE-OnRL MAE** | **QoE-OnRL E<sub>50</sub>** | **QoE-OnRL <br>E<sub>90</sub>** | **QoE-Loki MAE** | **QoE-Loki <br>E<sub>50</sub>** | **QoE-Loki <br>E<sub>90</sub>** | **QoE-R3Net MAE** | **QoE-R3Net E<sub>50</sub>** | **QoE-R3Net E<sub>90</sub>** | **Running Time** |
|------------------|------------------|------------------------------|------------------------------|-------------------|------------------------------|------------------------------|--------------------|------------------------------|------------------------------|-------------------|
| RF               | 56.89            | 37.23                        | 122.87                       | 0.227             | 0.169                        | 0.415                        | 1.772              | 1.341                        | 3.388                        | **0.14 ms**       |
| SVR              | 82.88            | 61.36                        | 163.89                       | 0.657             | 0.635                        | 0.855                        | 2.052              | 1.702                        | 3.757                        | **0.21 ms**       |
| DNN              | 55.32            | 31.43                        | 137.74                       | 0.233             | 0.139                        | 0.552                        | 1.618              | 1.215                        | 3.086                        | **0.59 ms**       |
| CNN-LSTM         | 53.02            | 29.85                        | 127.37                       | 0.214             | 0.133                        | 0.509                        | 1.555              | **1.152**                    | 3.086                        | **3.93 ms**       |
| TTPP, w/o aug    | 55.13            | 27.08                        | 138.28                       | 0.184             | **0.106**                    | 0.285                        | 1.616              | 1.176                        | 3.295                        | **4.30 ms**       |
| **TTPP (ours)**  | **46.39**        | **26.61**                    | **106.88**                   | **0.163**         | 0.107                        | **0.232**                    | **1.514**          | 1.171                        | **2.837**                    | **4.26 ms**       |

</div>

We also plotted the CDF of the absolute prediction error of the proposed scheme, as shown in Fig 4. Compared with the baseline algorithm, the absolute error of the TTPP algorithm proposed in this paper is reduced by 34.75 maximum and increased by 56.6%. In addition, below the 70th percentile, the CDF curve of the TTPP algorithm overlaps between the data enhancement method and the non-data enhancement method, while above the 70th percentile, the CDF curve of the TTPP algorithm with data enhancement shows better performance. The results show that data enhancement methods have performance advantages over non-data enhancement methods at higher percentiles.
<div align="center">
  
<img src="https://github.com/alen-quan/RIC-assisted-realtime-video-QoE-prediction-system/blob/main/Fig 4. CDF of absolute errors.png" width ="600"  alt="Fig. 4. CDF of absolute errors">

</div>

<p align="center">Fig. 4. CDF of absolute errors for different prediction schemes.</p>
