# Ecobloom Ecogarden - Simple Home Assistant Integration

The EcoGarden™ is Ecobloom’s first product initially launched on Kickstarter in 2018. It utilizes an ancient growing technique known as aquaponics, which uses fish waste as a nutrient source for the plants, while the plants naturally filter the water which is recirculated back to the fish. It’s a natural and effective way of creating the ultimate self-sustaining and resource-efficient ecosystem where plants and fish live in symbiosis.

More information on the Ecogarden by Ecobloom: https://ecobloom.se/ecogarden/

This Github describes the integration of the Ecobloom Ecogarden into Home Assistant through a local API.

More information on Home Assistant: https://homeassistant.io

The following features have been implemented:
  - Automations:
    - 
    - Feed the fish at 9am (unless already fed manually earlier)
    - Reset the 'fish already fed check'

  - Scripts:
    -
    - Manually feed the fish (and turn on the 'fish already fed check')

  - Shell Commands:
    -
    - Feed Fish (shell_command.ecogarden_feedfish)

  - Helpers:
    - 
    - Fish already fed check (input_boolean.aquarium_fish_fed)

    Helpers are created in the HA back-office (Configuration > Automations & Scenes > Helpers)

----
## Disclaimer

This is not an official Home Assistant integration.   The information shared in this Github is a representation of how I integrated the Ecobloom Ecogarden into my own Home Assistant environment.   Don't simply copy/paste my examples into your personal HA instance as it will most likely not work "just like that".  

Also, I am not affiliated with Ecobloom in any way.   As the official Ecogarden app is currently only providing limited functionality, I've contacted Ecobloom with the request for a local API to allow integration with Home Assistant.  As a token of appreciation towards Ecobloom for providing this API, I am sharing my Ecogarden configuration on Github and on the Home Assistant Community page for other HA users to benefit from.    Special thanks to Robin and Matthew of Ecobloom for their positive reaction to my request.
