## Build tools and dependencies
```shell
# Install dependencies
sudo apt-get install cmake make gcc g++ pkg-config libfftw3-dev libmbedtls-dev libsctp-dev libyaml-cpp-dev libgtest-dev libboost-program-options-dev libconfig++-dev

git clone https://github.com/srsran/srsRAN_4G.git
cd srsRAN_4G
mkdir build
cd build
cmake ..
make
# Optional
make test

sudo make install
```

## Install RF drivers
- We need to install [RF drivers](https://files.ettus.com/manual/page_install.html) to support different radio types. Currently, only UHD is supported by srsRAN.
```shell
sudo apt-get install libuhd-dev uhd-host
```

- Download UHD images from Internet to the machine. If not, you may get the error `[WARNING] [B200] EnvironmentError: IOError: Could not find path for image: usrp_b200_fw.hex`
```shell
sudo /usr/lib/uhd/utils/uhd_images_downloader.py
```

## Understanding of srsRAN ENB config file
- We should pay attention to the IP addresses in the enb configuration. For instance, while `mme_addr` is similar to VM's IP, here `172.16.0.10`, `gtp_bind_addr` and `s1c_bind_addr` are similar to the machine's IP, here `172.10.0.2`. Otherwise, we will fail to initiate NG connection between 5G core running on Virtual Box and srsRAN.
```
[enb] # enb configuration
enb_id = 0x19B
mcc = 001
mnc = 01
mme_addr      = 172.16.0.10 # IP address of MME for S1 connnection
gtp_bind_addr = 172.16.0.2 # Local IP address to bind for GTP connection
s1c_bind_addr = 172.16.0.2 # Local IP address to bind for S1AP connection

s1c_bind_port = 0
n_prb = 50

[pcap] # output some pcap files for debugging
enable = true
filename = /tmp/enb_mac.pcap
nr_filename = /tmp/enb_mac.pcap

[log] # log configuration
all_level = info # levels: debug, info, warning, error, none
all_hex_limit = 32
filename = /tmp/enb.log
file_max_size = -1

[expert] # can output some metrics
metrics_csv_enable   = true
metrics_csv_filename = /tmp/enb_metrics.csv
report_json_enable   = true
report_json_filename = /tmp/enb_report.js
```

- To fix the static IP address of the machine, running the following command:
```shell
sudo ifconfig vboxnet0 172.16.0.2
```

## Running srsRAN ENB
```shell
$ sudo srsenb enb-open5gs.conf
Active RF plugins: libsrsran_rf_uhd.so
Inactive RF plugins: 
---  Software Radio Systems LTE eNodeB  ---

Reading configuration file enb-open5gs.conf...
WARNING: cpu0 scaling governor is not set to performance mode. Realtime processing could be compromised. Consider setting it to performance mode before running the application.

Built in Release mode using commit 254cc719a on branch master.

Opening 1 channels in RF device=default with args=default
Supported RF device list: UHD file
Trying to open RF device 'UHD'
[INFO] [UHD] linux; GNU C++ version 9.2.1 20200304; Boost_107100; UHD_3.15.0.0-2build5
[INFO] [LOGGING] NG connection successful
Fastpath logging disabled at runtime.
Opening USRP channels=1, args: type=b200,master_clock_rate=23.04e6
[INFO] [UHD RF] RF UHD Generic instance constructed
[INFO] [B200] Detected Device: B210
[INFO] [B200] Operating over USB 3.
[INFO] [B200] Initialize CODEC control...
[INFO] [B200] Initialize Radio control...
[INFO] [B200] Performing register loopback test... 
[INFO] [B200] Register loopback test passed
[INFO] [B200] Performing register loopback test... 
[INFO] [B200] Register loopback test passed
[INFO] [B200] Asking for clock rate 23.040000 MHz... 
[INFO] [B200] Actually got clock rate 23.040000 MHz.
RF device 'UHD' successfully opened

==== eNodeB started ===
Type <t> to view trace
Setting frequency: DL=1842.5 Mhz, DL_SSB=1842.05 Mhz (SSB-ARFCN=368410), UL=1747.5 MHz for cc_idx=0 nof_prb=52
t
Enter t to stop trace.
RACH:  slot=7531, cc=0, preamble=4, offset=0, temp_crnti=0x4601

               -----------------DL----------------|-------------------------UL-------------------------
rat  pci rnti  cqi  ri  mcs  brate   ok  nok  (%) | pusch  pucch  phr  mcs  brate   ok  nok  (%)    bsr
 nr    0 4601   11   0    5    89k   18    0   0% |  20.6    8.9    0    4    72k   14    0   0%    0.0
 nr    0 4601   12   0    5   558k  121    0   0% |  20.6   14.0    0    5   435k   85    0   0%    0.0
 nr    0 4601   11   0    0      0    0    0   0% |   n/a   -2.2    0    0      0    0    0   0%    0.0
 nr    0 4601    7   0    0      0    0    0   0% |   n/a   -1.5    0    0      0    0    0   0%    0.0
 nr    0 4601    7   0    0      0    0    0   0% |   n/a   -2.1    0    0      0    0    0   0%    0.0
 nr    0 4601    8   0    0      0    0    0   0% |   n/a   -1.5    0    0      0    0    0   0%    0.0
 nr    0 4601   11   0    5   272k   59    0   0% |  20.7    9.2    0    5   133k   26    0   0%    0.0
 nr    0 4601    9   0    5   2.1M  457    0   0% |  20.8   14.9    0    5   548k  107    0   0%    0.0
 nr    0 4601   11   0    5   1.4M  305    0   0% |  20.7   14.7    0    5   364k   71    0   0%    0.0
 nr    0 4601   12   0    5   230k   50    0   0% |  20.6   10.2    0    5   343k   67    0   0%    0.0
 nr    0 4601   12   0    5   4.6k    1    0   0% |  20.5   -1.9    0    5   5.1k    1    0   0%    0.0
```
