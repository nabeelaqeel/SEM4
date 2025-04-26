

### Rename Adapter
Open PowerShell as Administrator:

Press Start, type powershell, right-click it, and select Run as administrator.

Run this command to list adapters:

```powershell
Get-NetAdapter
```


Rename it:
```
Rename-NetAdapter -Name "TAP-Windows Adapter V9" -NewName "VME1"
```

```
country=US  # Replace with your country code (e.g., GB, DE, IN)
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

# First network (highest priority)
network={
    ssid="WifiRumahSewa_5GHz"
    psk="ahmadtaufiq1474"
    key_mgmt=WPA-PSK
    priority=1  # Higher priority = tries first
}

# Second network (backup)
network={
    ssid="Redmi Note 11 Pro"
    psk="kenapa_pulak5"
    key_mgmt=WPA-PSK
    priority=2  # Lower priority = tries if first fails
}

```


Enable VNC and SSH 
```
sudo raspi-config
```

# Jupiter Lab 
https://medium.com/analytics-vidhya/jupyter-lab-on-raspberry-pi-22876591b227

```
sudo apt-get update  
sudo apt-get install python3-pip  
sudo pip3 install setuptools  
sudo apt install libffi-dev  
sudo pip3 install cffi
```

```
pip3 install jupyterlab
```

Got issue then do this
```
# Update package lists
sudo apt update

# Install build tools and dependencies
sudo apt install -y build-essential libzmq3-dev python3-dev

# Ensure pip is up-to-date
python3 -m pip install --upgrade pip
```

```
mkdir notebooks  
jupyter lab --notebook-dir=~/notebooks
```

```
jupyter lab
```



```
export PATH=$PATH:~/.local/bin
echo 'export PATH=$PATH:~/.local/bin' >> ~/.bashrc
source ~/.bashrc
```

```
which jupyter-lab
```

> /home/user/.local/bin/jupyter-lab

```
sudo nano /etc/systemd/system/jupyter.service
```

> [!NOTE]- /etc/systemd/system/jupyter.service
> ```
> [Unit]
> Description=Jupyter Lab
> After=network.target
> 
> [Service]
> Type=simple
> User=user
> Group=user
> WorkingDirectory=/home/user/notebooks
> ExecStart=/home/user/.local/bin/jupyter-lab --ip=0.0.0.0 --no-browser --notebook-dir=/home/user/notebooks
> Restart=always
> RestartSec=10
> Environment="PATH=/home/user/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
> 
> [Install]
> WantedBy=multi-user.target
> ```

```
sudo systemctl enable jupyter.service  
sudo systemctl daemon-reload
```

```
sudo systemctl start jupyter.service
```

To stop
```
sudo systemctl stop jupyter.service
```

check status
```
sudo systemctl status jupyter.service
```


```
sudo chown -R $USER:$USER ~/.jupyter
sudo chown -R $USER:$USER ~/.local/share/jupyter
```

[!NOTE]- /etc/wpa_supplicant/wpa_supplicant.conf
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
        ssid="WifiRumahSewa_5GHz"
		psk=9f8aec21a58144e0a4be12bb51f680a24d929b46bd0c5fc22dfe66826fb5f090
}


network={
        ssid="Acrylic_Paint"
        psk=kambing123
}



```


```
iwgetid wlan0
```

sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

Troubleshoot
```
sudo wpa_cli -i wlan0 status
```

```
sudo wpa_cli -i wlan0 reconfigure
```

```
sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
```