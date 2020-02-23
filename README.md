Simple envirenment for java / hybris development.

Currently the environment aims for german users only. please review keyboard settings (Vagrantfile / 20-keyboard.conf) and review the installed eclipse plugins.

Usage (first time):
start the system using ''vagrant up''. After completing the install process restart the system (''vagrant halt'' and ''vagrant up'' again)


## Required addons / prerequirements
> vagrant plugins install vagrant-disksize
> vagrant plugins install vagrant-vbguest
> vagrant plugins install vagrant-certificates

## Install process
after the initial process the machine is prepaired for normal usage and does not need the additonal reboot. Use 
    vagrant up 
to start the system and 
    vagrant halt
to stop the system.
