# Ecobloom Ecogarden - Simple Home Assistant Integration

![Ecobloom Ecogarden](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/ecogarden.png)

The [EcoGarden™](https://ecobloom.se/ecogarden/) is Ecobloom’s first product initially launched on Kickstarter in 2018. It utilizes an ancient growing technique known as aquaponics, which uses fish waste as a nutrient source for the plants, while the plants naturally filter the water which is recirculated back to the fish. It’s a natural and effective way of creating the ultimate self-sustaining and resource-efficient ecosystem where plants and fish live in symbiosis.

![Aquaponics](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/aquaponics.png)

This Github describes the integration of the Ecobloom Ecogarden into [Home Assistant](https://homeassistant.io/) (HA) through a local API.

Home Assistant is a free and open-source software for home automation that is designed to be the central control system for smart home devices with focus on local control and privacy. It can be accessed via a web-based user interface, via companion apps for Android and iOS, or using voice commands via a supported virtual assistant like Google Assistant and Amazon Alexa.  Click [here](https://demo.home-assistant.io/#/lovelace/0) for a demo.

I am using a combination of shell commands (to send commands to the Ecogarden, e.g. feed the fish) and RESTful sensors (to receive current values, e.g.  water temperature).   These are then used in a number of scripts and automations to allow automatic actions and voice commands through Google Home (other voice assistants can be used as well).  Current status of the aquarium and actions can also be triggered manually via the Lovelace back-office.   

The following features have been implemented:

  - [Shell Commands](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/shell%20commands) [:grey_question:](https://www.home-assistant.io/integrations/shell_command/)
    -
    - Feed Fish (shell_command.ecogarden_feedfish)


  - [Sensors](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/sensors)
    -     
    #### RESTful Sensors [:grey_question:](https://www.home-assistant.io/integrations/sensor.rest/)
    - Temperature of the water (sensor.ecogarden_water_temperature)
    - Ambient light sensor (sensor.ecogarden_light_sensor)
    
     #### Template Sensors [:grey_question:](https://www.home-assistant.io/integrations/template/)
    - Sensor to show status fish feeding in a user-friendly way (sensor.template_aquarium_fish_fed)
 
 
  - [Automations](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/automations) [:grey_question:](https://www.home-assistant.io/docs/automation/basics/)
    -     
    - Feed the fish at 9am unless already fed manually earlier (automation.aquarium_feed_fish_at_9am)
    - Reset the 'fish already fed check' at midnight to allow automatic feeding the next day (automation.aquarium_reset_feed_fish_check)

  - [Scripts](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/scripts) [:grey_question:](https://www.home-assistant.io/integrations/script/)
    -
    - Manually feed the fish and turn on the 'fish already fed check' (script.aquarium_feed_fish_manually)


  - Helpers
    - 
    - Fish already fed check (input_boolean.aquarium_fish_fed)

    Helpers are created in the HA back-office (Configuration > Automations & Scenes > Helpers)
  
  
  - [Lovelace Back-Office](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/lovelace)
    - 
![Lovelace Card](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/lovelace%20card.png)
 
 
  - Google Assistant / Google Home Integration [:grey_question:](https://www.home-assistant.io/integrations/google_assistant/)
    - 
    The below steps only work if you have already set up a working connection between your HA environment and Google Assistant.
    
    #### Fish Feeding [:movie_camera:](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/movies/GH_fish_feeding.mov)
    - Ensure that the script 'script.aquarium_feed_fish_manually' is exposed within the Google Assistant settings of your HA environment (Configuration > Home Assistant Cloud > Google Assistant > Manage Entities)
    - Once exposed, the script appears as a scene in the Google Assistant app
    - Feed the fish with the command: 'Hey Google, Activate Fish Feeding'
    - Alternatively you can also create a routine that reacts to voice command 'Hey Google, Feed The Fish' and which then automatically activates the 'Activate Fish Feeding' scene.

    ![Routine Example](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/routine_example.PNG)


  - Extra's
    - 
    To further enhance the experience of the Ecogarden, I'm also using the following tools, which are integrated into HA as well.
    
    - As the Ecogarden only has a led lamp above the plants but not in the aquarium itself, I've added an aquarium specific light solution myself.  To be able to automatically turn the aquarium lights on and off (based on presence, time of day, etc..), I am using a [Z-Wave](https://www.home-assistant.io/integrations/zwave_js/) Smart Switch.

  - Next Steps
    - 
    Potential further improvements, possible in HA (but not implemented yet)
    
    - Warning (on smartphone, in back-office, via Voice Assistant, ...) when the water temperature goes above/below certain tresholds.
    - Warning when fish are not fed yet after a certain time of the day.
    - Warning when someone manually feeds the fish when they got food already.
    - Automatically turn on/off the aquarium light based on home presence, time of day, ...
    - Warning when the aquarium light is on at night or when nobody is home.
    - ...

----
# Disclaimer

This is not an official Home Assistant integration.   The information shared in this Github is a representation of how I integrated the Ecobloom Ecogarden into my own Home Assistant environment.   Don't simply copy/paste my examples into your personal HA instance as it will most likely not work "just like that".  

Also, I am not affiliated with Ecobloom in any way.   As the official Ecogarden app is currently only providing limited functionality, I've contacted Ecobloom with the request for a local API to allow integration with Home Assistant.  As a token of appreciation towards Ecobloom for providing this API, I am sharing my Ecogarden configuration on Github and on the Home Assistant Community page for other HA users to benefit from.    Special thanks to Robyn and Matt of Ecobloom for their positive reaction to my request.
