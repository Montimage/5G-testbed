# 5G-testbed
This repository contains a step-by-step guide for deploying a 5G testbed using existing open-source tools and technologies. In addition to the deployment guide, this repository also shows how we create a dataset of raw network traffic from the 5G testbed and analyzing it using our AI-based applications in some context, such as mobile activities classification for security and network optimization. Furthermore, we collect and provide links to additional resources and documentation that may be useful in deploying and testing a 5G testbed.

We hope that this project will be helpful for anyone interested in experimenting with 5G technology. If you have any questions or feedback, please feel free to open an issue or submit a pull request.

## Requirements
The guide assumes that you have access to the necessary hardware and software components, including:
- [**OnePlus Nord 5G phone**](https://www.oneplus.com/fr/nord-ce-5g/specs)
- [**USRP B210**](https://www.ettus.com/all-products/ub210-kit/) is a type of software-defined radio (SDR) platform that is ideal for a variety of applications, including wireless communication research, spectrum analysis, and general-purpose software radio experimentation. It has two receive and two transmit channels, each capable of up to 56 MHz of instantaneous bandwidth. The USRP B210 is capable of operating over a wide frequency range, from 70 MHz to 6 GHz, and can be used with a variety of software frameworks, including GNU Radio, MATLAB, and LabVIEW.
- **SRSRAN** is an open-source software suite serving as a Radio Access Network (RAN) for 4G/5G cellular networks. It is installed on a machine or a server, running Ubuntu version 20.04 (see [installation guide](./srsRAN.md)).
- **Open5GS** is an open-source software suite that serves as a 5G core network for 5G cellular networks. It should be installed on a Virtual Machine (VM) running Ubuntu 20.04 on Virtual Box (see [installation guide](./open5gs.md)).
- **Montimage Monitoring Tool (MMT)** is an open-source framework designed for monitoring and analyzing network traffic, including 4G/5G and IoT (see [installation guide](./mmt.md)).

