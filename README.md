# RIC-assisted-realtime-video-QoE-prediction-system
## It's a test 
_Y. Sun, W. Xiong, G. Pan,S. Xu, S. Zhang and X. Chen.QoE Prediction in RIC-assisted Wireless Real-time Video Transmission System with Transformer, Submitted to IEEE Transactions on Vehicular Technology._

This is the Github repository which provides a detailed introduction to the experimental environment and data acquisition process of this letter. The main aim of the repository is to present our RIC-assisted realtime video QoE prediction system, discuss and report issues. This demo showcases the architecture of the system and the process of obtaining data. All the experiments mentioned in the letter are based on the datasets collected on the prototype platform. 
## Experimental environment
Our proposed prediction scheme has been tested on our prototype communication platform based on OpenAirInterface (OAI) and a real-time video transmission platform based on Web Real-Time Communication (WebRTC). The communication platform consists of a software-defined Evolved Packet Core (EPC) and Radio Access Network (RAN), a RIC platform, a Radio Frequency Front-end (USRP) B210, and commercial User Equipment (UE). The real-time video transmission platform is composed of a server and client side, as illustrated in the figure below.

The system can interconnect with commercial User Equipment (UE) and provide them with a cellular network for data transmission. The UE receives video sent by the video server and obtains Quality of Experience (QoE) related information from the server. Concurrently, it can acquire bandwidth-related Radio Access Network (RAN) information from the RAN side through the Mobile Edge Computing (MEC) server and generate datasets.

<div align="center">
  
  <img src="https://github.com/alen-quan/RIC-assisted-realtime-video-QoE-prediction-system/blob/main/Fig 1. Experimental Environment.png" width ="600" alt="Environment">
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
  RIC|Intel i7-8559U|Edgegallery|
  WebRTC server|Intel i9-9980HK|WebRTC|
  Radio Frequency Front-End|Ettus USRP B210|N/A|
  UEs|6×Huawei Nexus 6P|Android 8.0|
  
  </div>
  
## Data Collection
  we collect datasets under the following three different transmission conditions based on the edge-assisted wireless communication system.
  ### Configuration Cases
  * Case1: The UE is close to the usrp, and the wireless network status is good.
  * Case2: The UE is far away from the usrp, and the wireless network status is poor
  * Case3: The UE is far away from the usrp, and the wireless network status is good and bad
### Process 

To generate datasets for different wireless environments, we have done the following implementation work. 
  * Firstly, we open the OAI system, including eNB and EPC (three core network elements, i.e., MME, HSS and SPGW). 
  * Secondly, we switch the commercial UEs from airplane mode to non-airplane mode. The UEs are connected to the cellular network as shown in the figure below.
  * Thirdly, The UE receives and plays real-time video from the WebRTC server, and the video bit rate is automatically selected according to the network status.
  * Fourthly, the RIC server collects the RAN information through the flexRAN feedback during the $t$-th transmission period and saves them to the dataset according to a certain format. And WebRTC server records real-time video QOE-related information and generates datasets to send to the RIC. The details of RAN information are listed in the following table.

The data set collected in the above steps will be trained and tested on the RIC. 

The data training process is performed on the RIC using the Pytorch platform. When the offline training process is complete, the video stream QoE prediction model is hosted on the RIC. The proposed prediction scheme and baseline prediction scheme obtain the RAN context measurement results and video QoE information of the previous $t_p$ = 4 transmission cycles, and predict the video stream QoE of the next transmission cycle.

## Experimental Result
