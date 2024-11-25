# RIC-assisted-realtime-video-QoE-prediction-system
## It's a test 
_Y. Sun, W. Xiong, G. Pan,S. Xu, S. Zhang and X. Chen.QoE Prediction in RIC-assisted Wireless Real-time Video Transmission System with Transformer, Submitted to IEEE Transactions on Vehicular Technology._

This is the Github repository which provides a detailed introduction to the experimental environment and data acquisition process of this letter. The main aim of the repository is to present our RIC-assisted realtime video QoE prediction system, discuss and report issues. This demo showcases the architecture of the system and the process of obtaining data. All the experiments mentioned in the letter are based on the datasets collected on the prototype platform. 
## Experimental environment
Our proposed prediction scheme has been tested on our prototype communication platform based on OpenAirInterface (OAI) and a real-time video transmission platform based on Web Real-Time Communication (WebRTC). The communication platform consists of a software-defined Evolved Packet Core (EPC) and Radio Access Network (RAN), a Mobile Edge Computing (MEC) platform, a Radio Frequency Front-end (USRP) B210, and commercial User Equipment (UE). The real-time video transmission platform is composed of a server and client side, as illustrated in the figure below.

The system can interconnect with commercial User Equipment (UE) and provide them with a cellular network for data transmission. The UE receives video sent by the video server and obtains Quality of Experience (QoE) related information from the server. Concurrently, it can acquire bandwidth-related Radio Access Network (RAN) information from the RAN side through the Mobile Edge Computing (MEC) server and generate datasets.
## Data Collection
