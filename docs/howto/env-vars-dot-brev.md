# How To
## Environment Variables in the Setup Script

[The .brev scripts](/reference/dot-brev-setup-script) executes once a Brev machine is provisioned, but are not preserved. You must instead add environment variables to a `~/.bashrc` or `~/.zshrc` file that gets sourced. 


For example, to install python's package manager pip which requires modifying the path, you'll need to first install pip:

```zsh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
rm get-pip.py
```

You'll need to instead put this new path in your zshrc and bashrc and source both files.
```zsh
printf "\n%s\n" "export PATH=/home/brev/.local/bin:$PATH" | tee -a ~/.bashrc | tee -a ~/.zshrc

# Instead of exporting the variable:
# export PATH=/home/brev/.local/bin:$PATH 

```


Here's the full snipped to add to .brev for properly installing pip:

```zsh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
rm get-pip.py

echo "" >> ~/.zshrc
echo "export PATH=/home/brev/.local/bin:$PATH" >> ~/.zshrc
echo "" >> ~/.bashrc
echo "export PATH=/home/brev/.local/bin:$PATH" >> ~/.bashrc
source ~/.zshrc
source ~/.bashrc
```