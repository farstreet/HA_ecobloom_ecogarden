# Ecobloom Ecogarden - Simple Home Assistant Integration

The EcoGarden™ is Ecobloom’s first product initially launched on Kickstarter in 2018. It utilizes an ancient growing technique known as aquaponics, which uses fish waste as a nutrient source for the plants, while the plants naturally filter the water which is recirculated back to the fish. It’s a natural and effective way of creating the ultimate self-sustaining and resource-efficient ecosystem where plants and fish live in symbiosis.

More information on the Ecogarden by Ecobloom: https://ecobloom.se/ecogarden/

This Github describes the integration of the Ecobloom Ecogarden into Home Assistant through a local API.

I am using a combination of shell commands (to send commands to the Ecogarden, e.g. feed the fish) and RESTful sensors (to receive current values, e.g.  water temperature).   These are then used in a number of scripts and automations to allow automatic actions and voice commands through Google Home (other voice assistants can be used as well).  Current status of the aquarium and actions can also be triggered manually via the Lovelace back-office.   

More information on Home Assistant: https://homeassistant.io

The following features have been implemented:

  - Shell Commands [:grey_question:](https://www.home-assistant.io/integrations/shell_command/)
    -
    - Feed Fish (shell_command.ecogarden_feedfish)
    
  - Sensors
    -     
    ### RESTful Sensors [:grey_question:](https://www.home-assistant.io/integrations/sensor.rest/)
    - Temperature of the water (sensor.ecogarden_water_temperature)
    - Ambient light sensor (sensor.ecogarden_light_sensor)
    
     ### Template Sensors [:grey_question:](https://www.home-assistant.io/integrations/template/)
    - Sensor to show status fish feeding in a user-friendly way (sensor.template_aquarium_fish_fed)
    
  - Automations [:grey_question:](https://www.home-assistant.io/docs/automation/basics/)
    -     
    - Feed the fish at 9am unless already fed manually earlier (automation.aquarium_feed_fish_at_9am)
    - Reset the 'fish already fed check' at midnight to allow automatic feeding the next day (automation.aquarium_reset_feed_fish_check)

  - Scripts [:grey_question:](https://www.home-assistant.io/integrations/script/)
    -
    - Manually feed the fish and turn on the 'fish already fed check' (script.aquarium_feed_fish_manually)

  - Helpers
    - 
    - Fish already fed check (input_boolean.aquarium_fish_fed)

    Helpers are created in the HA back-office (Configuration > Automations & Scenes > Helpers)
    
  - Lovelace Back-Office
    - 
    - Button Card to feed the fish manually from the Back-office
    
  - Google Assistant / Google Home Integration [:grey_question:](https://www.home-assistant.io/integrations/google_assistant/)
    - 
    The below steps only work if you have already set up a working connection between your HA environment and Google Assistant.
    
    ### Fish Feeding
    - Ensure that the script 'script.aquarium_feed_fish_manually' is exposed within the Google Assistant settings of your HA environment (Configuration > Home Assistant Cloud > Google Assistant > Manage Entities)
    - Once exposed, the script appears as a scene in the Google Assistant app
    - Feed the fish with the command: 'OK Google, Activate Fish Feeding'


----
## Disclaimer

This is not an official Home Assistant integration.   The information shared in this Github is a representation of how I integrated the Ecobloom Ecogarden into my own Home Assistant environment.   Don't simply copy/paste my examples into your personal HA instance as it will most likely not work "just like that".  

Also, I am not affiliated with Ecobloom in any way.   As the official Ecogarden app is currently only providing limited functionality, I've contacted Ecobloom with the request for a local API to allow integration with Home Assistant.  As a token of appreciation towards Ecobloom for providing this API, I am sharing my Ecogarden configuration on Github and on the Home Assistant Community page for other HA users to benefit from.    Special thanks to Robin and Matthew of Ecobloom for their positive reaction to my request.
