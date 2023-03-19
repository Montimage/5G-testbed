## Install MMT tools

### mmt-dpi

### mmt-security

### mmt-probe

### mmt-operator

```shell
# Install mongodb version 4.4
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
sudo apt-get update
sudo apt-get install -y mongodb-org=4.4.19 mongodb-org-server=4.4.19 mongodb-org-shell=4.4.19 mongodb-org-mongos=4.4.19 mongodb-org-tools=4.4.19
sudo systemctl start mongod
sudo systemctl status mongod

# Checkout the project and run mmt-operator
git clone https://github.com/Montimage/mmt-operator.git
cd mmt-operator/www
sudo node bin/www
```

## Analyze 5G network traffic using MMT tools
TODO
