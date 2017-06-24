## Portus

### Install

1. `apt-get install docker.io docker-compose`
2. `git clone https://github.com/SUSE/Portus.git`
3. `cd Portus`
4. `./compose-setup.sh -e 192.168.116.9`

### Fix Install
According to this [issue](https://github.com/SUSE/Portus/issues/1245)

#### 1. Install NPM
1. Upgrade nodejs version: `curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -`
1. `sudo apt-get install nodejs`
1. `sudo apt-get install npm`

If fails, find a way in this [blog](https://linuxconfig.org/how-to-install-node-js-on-ubuntu-16-04-xenial-xerus-linux-server#h5-2-using-ppa-repository)

#### 2. Fix Portus
In `Protus` path, run as root: `sudo -s`
If yarn install fails, run several more times

1. `npm install -g webpack yarn --registry=https://registry.npm.taobao.org`
1. `sudo ln -s /usr/bin/nodejs /usr/bin/node`
1. `yarn install --registry=https://registry.npm.taobao.org`
1. `webpack --watch --config config/webpack.js`



