
# Experiment: Setup a Linux Based Lilypad Resource Provider with no GPU attached

This is an experiment to see what happens when an individual sets up a lilypad resource-provider without a GPU attached. After doing the experiment, it seems like if you try to setup a lilypad RP without a Nvidia GPU, you will not be able to start the Lilypad RP service. 

 Step 1. Setup a linux box(Ubuntu 22.04) and configure a wallet with Arbitrum and LP tokens/funds. 

 Step 2. Install Nvidia Container Toolkit and Drivers(cannot install NVidia Drivers bc there is no GPU attached)

 Step 3. Setup the systemd unit's for GPU provider

    - I made sure to leave the "Environment" GPU var set to 1

 Step 4. Turn on the services(lilypad+bacalhau)

    `systemctl start lilypad-resource-provider.service`
    `systemctl start bacalhau.service`

Step 5. Check the system logs to see what the services are doing

    `sudo journalctl -u lilypad-resource-provider.service -f`
    `sudo journalctl -u bacalhau.service -f`

Conclusion. After attempting to start the services up- I am getting an error stating- This means that if you're not running a GPU- the Lilypad RP will not startup for you. 

![Screenshot from 2024-08-18 16-35-20](https://github.com/user-attachments/assets/c2b84282-cbca-4efc-931c-56da21257eb7)

`lilypad [8150]: /usr/local/bin/lilypad: error while loading shared libraries: libcuda.so.1: cannot open shared object file: No such file or directory
systemd [1]:
lilypad- resource-provider.service: Main process exited, code=exited, status=127/n/a
systemd [1]:`

 Extra Steps.

Attempt this while setting the GPU var to zero within the RP Provider Variables
![Screenshot from 2024-08-18 16-43-15](https://github.com/user-attachments/assets/27fdedac-f610-401f-af17-15fe42310622)

Side Notes: I should try this again while also installing the nvidia drivers and then see what happens. Make sure setting the GPU to zero works for CPU Resource-Providers. 
```
