Simple development env for hybris development

Currently the environment aims for german users only. please review keyboard settings (Vagrantfile / 20-keyboard.conf) and review the installed eclipse plugins.

Usage (first time):
start the system using 

    vagrant up
    cd /vagrant
    # edit specific to your project
    # keep in mind: the exepected repository should contain hybris as within the repository root
    # by default only the hybris diretory of the hybris suite will be extracted. 
    vim project.properties 
    ant
    
After completing the install process restart the system (

    vagrant halt
    vagrant up

again.

After the initial process the machine is prepaired for normal usage and does not need the additonal reboot. Use 

    vagrant up 

to start the system and 

    vagrant halt

to stop the system.
