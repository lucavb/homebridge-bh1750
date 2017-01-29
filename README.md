# homebridge-hc-sr501
Homebridge plugin for the bh1750 light sensor on a Raspberry Pi

## Installation of other plugins

I assume that this [Guide](https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi) was followed, so your homebridge config file is under /var/homebridge and you used the systemd version. Create a folder called other_plugins in that hombridge folder and checkout this repository inside that newly created folder.

Now you want to alter the file you placed under /etc/default/homebridge accordingly

```
# Defaults / Configuration options for homebridge
# The following settings tells homebridge where to find the config.json file an$
#HOMEBRIDGE_OPTS=-U /var/homebridge
HOMEBRIDGE_OPTS=-U /var/homebridge -P /var/homebridge/other_plugins -D

# If you uncomment the following line, homebridge will log more
# You can display this via systemd's journalctl: journalctl -f -u homebridge
#DEBUG=*
```

You might need to run a systemctl command to update the config file. The system should inform you about the specific comand if you enter ``sudo service hombridge stop``. After you have executed the suggested command you'll want to enter ``sudo service hombridge restart``. Homebridge should now be aware of any additional plugins within the /var/hombridge/other_plugins folder.

Now run the following code to install the dependencies.

```
cd /var/hombridge/other_plugins/homebridge-bh1750
npm i
```

You can now add the configuration to your config.json

## Configuration

This is an example configuration file

```
{
    "accessory" : "bh1750",
    "name" : "BH1750FVI Light Sensor",
    "serial" : "6B4A3603-1EC9-4965-8A3F-F84887C2C90C",
    "model" : "BH1750FVI",
    "autoRefresh" : 300
}
```

| Key           | Description                                                                        |
|---------------|------------------------------------------------------------------------------------|
| accessory     | Required. Has to be "bh1750"                                             |
| name          | Required. The name of this accessory. This will appear in your homekit app         |
| serial         | Optional. The serial number for this accessory. |
| model         | Optional. The model for this accessory. |
| autoRefresh         | Optional. The number of seconds until a new value is read from the sensor and pushed to HomeKit. |
