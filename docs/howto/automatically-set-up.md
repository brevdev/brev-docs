# How To
## Automatically set up Brev dev environments with a bash script.
Specify software and dependencies that are required for your project. Creating a bash script for each Brev project will standardize dependencies, packages and tools across all developers contributing to the same project (ex. Node v14, Yarn v1.22). We used Bash because we don't want to impose our preference on how you set up your dev environment. For example, if you use Docker, you can run Docker compose in your bash script.


Below are common installations for your convenience. Add them to your root project directory at `/.brev/setup.sh` or create a separate repo for setup scripts

### Install Yarn
```zsh
##### Yarn #####
(echo ""; echo "##### Yarn #####"; echo "";)
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install -y yarn
```

### Install Rust
```zsh
#### RUST #####
(echo ""; echo "##### Rust #####"; echo "";)
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

### Install Homebrew
```zsh
##### Homebrew #####
(echo ""; echo "##### Homebrew #####"; echo "";)
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash -
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> $HOME/.bash_profile
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> $HOME/.zshrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

### Node
```zsh
##### Node v14.x + npm #####
(echo ""; echo "##### Node v14.x + npm #####"; echo "";)
sudo apt install ca-certificates
curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### Install NPM Packages Without Sudo
Note: this might not work depending on your shell. We recommend installing globally with sudo. 
```zsh
# install npm packages globally without sudo
# modified from https://stackoverflow.com/questions/18088372/how-to-npm-install-global-not-as-root
mkdir "${HOME}/.npm-packages"
printf "prefix=${HOME}/.npm-packages" >> $HOME/.npmrc
cat <<EOF | tee -a ~/.bashrc | tee -a ~/.zshrc
NPM_PACKAGES="\${HOME}/.npm-packages"
NODE_PATH="\${NPM_PACKAGES}/lib/node_modules:\${NODE_PATH}"
PATH="\${NPM_PACKAGES}/bin:\${PATH}"
# Unset manpath so we can inherit from /etc/manpath via the `manpath`
# command
unset MANPATH # delete if you already modified MANPATH elsewhere in your config
MANPATH="\${NPM_PACKAGES}/share/man:\$(manpath)"
EOF
```

### Python, Pip, and Poetry
```zsh
##### Python + Pip + Poetry #####
(echo ""; echo "##### Python + Pip + Poetry #####"; echo "";)
sudo apt-get install -y python3-distutils
sudo apt-get install -y python3-apt
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
rm get-pip.py
echo "" >> ~/.zshrc
echo "export PATH=$HOME/.local/bin:$PATH" >> ~/.zshrc
echo "" >> ~/.bashrc
echo "export PATH=$HOME/.local/bin:$PATH" >> ~/.bashrc
source ~/.zshrc
source ~/.bashrc
source $HOME/.poetry/env
```

### Golang
```zsh
##### Golang v16x #####
(echo ""; echo "##### Golang v16x #####"; echo "";)
wget https://golang.org/dl/go1.16.7.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.16.7.linux-amd64.tar.gz
echo "" | sudo tee -a ~/.bashrc
echo "export PATH=\$PATH:/usr/local/go/bin" | sudo tee -a ~/.bashrc
source ~/.bashrc
echo "" | sudo tee -a ~/.zshrc
echo "export PATH=\$PATH:/usr/local/go/bin" | sudo tee -a ~/.zshrc
source ~/.zshrc
rm go1.16.7.linux-amd64.tar.gz
```

### Custom command example
We recommend the echo statement before any command for clearer output logs.
```zsh
##### Custom commands #####
(echo ""; echo "##### Custom commands #####"; echo "";)
npm install
```
