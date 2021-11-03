# Tutorial #1
## Automatically set up Brev machines with .brev setup script.
Specify software and dependencies that are required for your project. Creating a .brev setup script for each Brev project will standardize dependencies, packages and tools across all developers contributing to the same project (ex. Node v14, Yarn v1.22)



Below are common installations for your convenience. Add them to your root project directory at `/.brev/setup.sh`

### Install Yarn
```zsh
##### Yarn #####
(echo ""; echo "##### Yarn #####"; echo "";)
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install -y yarn
```

### Install Homebrew
```zsh
##### Homebrew #####
(echo ""; echo "##### Homebrew #####"; echo "";)
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash -
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/brev/.bash_profile
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/brev/.zshrc
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
echo "export PATH=/home/brev/.local/bin:$PATH" >> ~/.zshrc
echo "" >> ~/.bashrc
echo "export PATH=/home/brev/.local/bin:$PATH" >> ~/.bashrc
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
