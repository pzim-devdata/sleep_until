# Sleep Until

Sleep Until is a Bash script to wait for a specified astronomical event such as sunrise or sunset before continuing execution.

It automatically calculates the time of the event based on geographic location and suspends execution until the precise moment of the event today or the next day if the event has already happened.

## Installation

To install sleep_until, run one of the following commands. It will be automatically added to your PATH: 

```
sudo wget -O /usr/local/bin/sleep_until https://raw.githubusercontent.com/pzim-devdata/sleep_until/main/sleep_until
sudo chmod +x /usr/local/bin/sleep_until
```

Or

```
sudo curl -o /usr/local/bin/sleep_until https://raw.githubusercontent.com/pzim-devdata/sleep_until/main/sleep_until
sudo chmod +x /usr/local/bin/sleep_until
```

This will download the script directly into /usr/local/bin, making it available globally.

## Usage

Example to wait for sunset (You must specify an event as first argument):

```bash
sleep_until sunset
```

Supported astronomical events:

- sunrise
- sunset
- solar_noon
- civil_twilight_begin 
- civil_twilight_end
- nautical_twilight_begin
- nautical_twilight_end 
- astronomical_twilight_begin
- astronomical_twilight_end

## Customization

You can customize the script by opening it in a notepad and modifying it:

```bash
sudo gedit /usr/local/bin/sleep_until
```

- If you don't want to automatically retrieve your location based on you IP address (for example if you use an VPN), you can configure the latitude and the longitude directly in the script by adding at the beginning of the script:

```
lat=48.8567  # Your latitude  
long=2.3508 # Your longitude
```

- If you don't want to use an argument as parameter for specifying the sunset or sunrise..., you can configure the event you want to wait directly in the script by adding at the beginning of the script:

```
sunset_or_sunrise='sunrise'# sunrise or sunset or solar_noon or civil_twilight_begin or civil_twilight_end or nautical_twilight_begin or nautical_twilight_end or astronomical_twilight_begin or astronomical_twilight_end
```
Now you will just need to execute `wait_until` without argument to directly wait for sunrise in this example

## Examples

- Wait for sunrise to run a script:

```bash 
sleep_until sunrise && ./my_script.sh
```

- Wait for sunrise + 10 minutes (600 seconds) to run a script:

```bash 
sleep_until sunrise && sleep 600 && ./my_script.sh
```

- Run script at dawn:

```bash 
sleep_untill civil_twilight_start && ./my_script.sh  
```

- Schedule backup at solar noon:

```cron
0 * * * * sleep_untill solar_noon && ./backup.sh
```

- Schedule a morning task at civil dawn: 

```cron
0 * * * * sleep_until civil_twilight_begin && ~/morning_script.sh
```

- Suspend execution during the night:

```bash
while sleep_untill sunrise; do
  # Process to perform during day
done
```

- Close a Somfy shutter when the night is coming with the [tahoma program by pzim-devdata](https://github.com/pzim-devdata/tahoma):

```bash
sleep_until astronomical_twilight_start && tahoma close shutter ['shutter garden']
```

## Concrete case

An amateur astronomer wants to automate the taking of photos of stars at night. It uses sleep_until in its crontab to start its capture sequence only after astronomical dusk.

## Copyright

copyright © 2024 pzim-devdata

This project is under the MIT License - see the LICENSE file for details.

## Author

pzim-devdata
