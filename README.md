# Workflow with SSH keys
This is a workaround for making workflow to work with SSH keys and private keys passphrase. You will need **pythonista**, this workaround is probably possible with other apps than pythonista but you're on your own by doing so.

## 1. In Pythonista

### Paramiko
We need the module paramiko for this to work. Easiest way to install paramiko to pythonista is to use [StaSH](https://github.com/ywangd/stash). In the command window of pythonista type this to install StaSH

    import requests as r; exec(r.get('http://bit.ly/get-stash').text)
    
When the StaSH is installed, it tells you to restart Pythonista. Do that. In your local folder (eg *this Ipad*) in Pythonista you will find the script `launch_stash.py`
Run the script and you should have a shell access there (it opens in another tab), in the terminal write:
    
    pip install paramiko

### Private key passphrase
I asume you use private key passphrase, if you don't small modifications to the python script and workflow can be made to make it work. (see the end of this tutorial for modifications without private key passphrase)
Exist Stash by closing the tab. In the command window of Pythonista write

    import keychain
    keychain.set_password(SERVICE, ACCOUNT, PASSWORD)
    
SERVICE should be set to what you are using it for, eg. `'WorkFlowSSH'`, ACCOUNT I set it to my SSH username eg `'JohnDoe'` and PASSWORD is your private key passphrase eg `'SUPERSECURE_PASSPHRASE1'`. It should look like this

    
    import keychain
    keychain.set_password('WorkFlowSSH', 'JohnDoe', 'SUPERSECURE_PASSPHRASE1')

Import you private key to pythonista, I did it by coping it to pythonistas icloud-folder, then in pythonista **I moved it to the local folder in Pythonista (eg. This Ipad).** 

### SSH.py
Copy the code in SSH.py in this repo, and paste it in a folder inside your local folder in pythonista, eg. This Ipad.


### No private key passphrase
If you don't have a private key passphrase, I've made comments in SSH.py of which lines you should comment out/uncomment. Also remove the workflow-part stated below. I haven't tested this, but it *should* work.

## 2. In Workflow

### Import the workflow

    https://workflow.is/workflows/bed501f09b0b4476a650c356388410ea
    
### Add the dictionary in the workflow
In the dictionary, add your own settings, here's the descripton for each key

* **cmd**: your command you want to send to the terminal. It's already a string so send in `ls /` rather than `'ls /'`
* **host**: your hostnamne
* **port**: port
* **user**: SSH username
* **privatekey**: The name of your private key
* **kc_service**: The SERVICE you choose when you set the password to the keychain, eg. WorkFlowSSH above. *(Remove this if you don't use a passphrase)*
* **kc_account**: The ACCOUNT you chouse when you set the password to the keychain, eg. JohnDoe above. *(Remove this if you don't use a passphrase)*


You should be able to use workflow with SSH Keys now, let me know if it doesn't work.