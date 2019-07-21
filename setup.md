# Setup
This is a guide meant to explain how to install Mopidy, run it as a service,
and especially how to setup ALSAMixer.

## Install Mopidy
https://docs.mopidy.com/en/latest/installation/debian/

### Install dependencies

    sudo apt install mopidy-spotify
    sudo -H pip install mopidy-iris mopidy-alsamixer

## Run as service
https://docs.mopidy.com/en/latest/service/

## Pulseaudio
Do not forget the Configuring Pulseaudio section, seen in
https://docs.mopidy.com/en/latest/service/#configure-pulseaudio  
In addition, uncomment the following lines in /etc/pulse/default.pa

    load-module module-alsa-sink
    load-module module-alsa-source device=hw:0,0

With the last line having the correct audio device.
It might also be good to comment the configuration of bluetooth devices if they
are giving you trouble: 

    #load-module module-bluetooth-policy
    #load-module module-bluetooth-discover

## Fix alsa
Add the following lines in mopidy config (in system, /etc/mopidy/mopidy.conf)

    [audio]
    mixer = alsamixer
    output = alsasink

    [alsamixer]
    enabled = true
    card = 0
    control = Master
    min_volume = 0
    max_volume = 100
    volume_scale = log
