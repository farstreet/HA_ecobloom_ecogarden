# ecobloom_ecogarden

The EcoGarden™ is Ecobloom’s first product initially launched on Kickstarter in 2018. It utilizes an ancient growing technique known as aquaponics, which uses fish waste as a nutrient source for the plants, while the plants naturally filter the water which is recirculated back to the fish. It’s a natural and effective way of creating the ultimate self-sustaining and resource-efficient ecosystem where plants and fish live in symbiosis.

More information on the Ecogarden by Ecobloom: https://ecobloom.se/ecogarden/

This Github describes the integration of the Ecobloom Ecogarden into Home Assistant through a local API.

More information on Home Assistant: https://homeassistant.io

The following features have been implemented:
  - Automations:
    - 
    - Feed the fish at 9am (unless already fed manually earlier)
    - Reset the 'fish already fed check'

  - Services:
    -
    - Manually feed the fish (and turn on the 'fish already fed check')

  - Shell Commands:
    -
    - Feed Fish (shell_command.ecogarden_feedfish)

  - Helpers:
    - 
    - Fish already fed check (input_select.aquarium_fish_fed)
