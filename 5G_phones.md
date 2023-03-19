In some cases, we really need to configure a 5G phone (here OnePlus Nord CE 5G) so that it can connect to our 5G testbed.

## Configure OpenCell sim

In our case, we use an [OpenCell SIM](https://open-cells.com/index.php/sim-cards/). The OpenCell SIM is based on the Universal Integrated Circuit Card (UICC) standard and can be reprogrammed using an open source Linux tool [UICC commands](https://open-cells.com/index.php/uiccsim-programing/). In order to use the OpenCell SIM with a specific mobile network operator, you may need to reprogram it with the appropriate UICC commands to configure it for that network.

Some key parameters to set are:
- ADM code for the SIM, for instance `--adm 12345678`.
- IMSI should follow the format `9970xxx1`, which is similar to the Open5GS’s subscriber IMSI, for instance `--imsi 997000000000001`.
- Subscriber Key `--key` and Operator Key OPC `--opc` should be similar to the corresponding parameters of our Open5GS’s subscriber.
- `-spn` could be anything, for example “Orange”.

```shell
# Download source code
wget https://open-cells.com/d5138782a8739209ec5760865b1e53b0/uicc-v2.6.tgz
tar xf uicc-v2.6.tgz

# Compile
cd uicc-v2.6
make

# Insert the card in the reader and the reader in a USB socket
sudo ./program_uicc

# Read basic data in the card
sudo DEBUG=y ./program_uicc

# Perform the same, with trace: all data exchange with the UICC are printed
sudo ./program_uicc --help 

# Configure the sim, for instance
sudo ./program_uicc --adm 12345678 --imsi 997000000000001 --isdn 00000001 --acc 0001 --key 6874736969202073796d4b2079650a73 --opc 504f20634f6320504f50206363500a4f -spn "OpenCells01" --authenticate --noreadafter

# See current values of the sim
sudo ./program_uicc --adm 12345678
```

## Root the 5G phone
TODO
