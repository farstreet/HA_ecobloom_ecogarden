# Ecobloom Ecogarden - Simple Home Assistant Integration

![Ecobloom Ecogarden](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/ecogarden.png)

The [EcoGarden™](https://ecobloom.se/ecogarden/) is Ecobloom’s first product initially launched on Kickstarter in 2018. It utilizes an ancient growing technique known as aquaponics, which uses fish waste as a nutrient source for the plants, while the plants naturally filter the water which is recirculated back to the fish. It’s a natural and effective way of creating the ultimate self-sustaining and resource-efficient ecosystem where plants and fish live in symbiosis.

![Aquaponics](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/aquaponics.png)

This Github describes the integration of the Ecobloom Ecogarden into [Home Assistant](https://homeassistant.io/) (HA) through a local API.

Home Assistant is a free and open-source software for home automation that is designed to be the central control system for smart home devices with focus on local control and privacy. It can be accessed via a web-based user interface, via companion apps for Android and iOS, or using voice commands via a supported virtual assistant like Google Assistant and Amazon Alexa.  Click [here](https://demo.home-assistant.io/#/lovelace/0) for a demo.

I am using a combination of commands (to send commands to the Ecogarden, e.g. feed the fish) and sensors (to receive current values, e.g.  water temperature).   These are then used in a number of scripts and automations to allow automatic actions, perform checks and execute voice commands through Google Home (other voice assistants can be used as well).  Current status of the aquarium and actions can also be triggered manually via the HA back-office.   

This project is work-in-progress.  Ecobloom is still creating the endpoints that are necessary to be able to connect with the Ecogarden.  I am updating this repository as I receive new endpoints to test from them.   There is no versioning available for this project.

The following features have already been implemented:

  - [Shell Commands](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/shell%20commands) [:grey_question:](https://www.home-assistant.io/integrations/shell_command/)
    -
    - Feed Fish (shell_command.ecogarden_feedfish) which instructs to Ecogarden to activate the built-in Fish Feeder and stores the server response in a temporary text-file which is used to create a sensor tha allows to determine whether the command was succesful or not
    - Feed Fish Result Reset (shell_command.ecogarden_feedfish_result_reset) to reset a sensor that is used to check whether the above Fish Feeding instruction was succesfully received and executed by the Ecogarden
    - Set Plant Led Brightness (shell_command.ecogarden_set_plant_led_brightness) to manually set the brightness of the led above the plants, when not using the Ecogarden Power Save Mode
    - Ecogarden Power Save Mode (shell_command.ecogarden_power_save_mode) which allows to turn the Ecogarden Power Save Mode on or off


  - [Sensors](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/sensors)
    -     
    #### RESTful Sensors [:grey_question:](https://www.home-assistant.io/integrations/sensor.rest/)
    - Temperature of the water (sensor.ecogarden_water_temperature)
    - Ambient light sensor (sensor.ecogarden_light_sensor)
    
     #### Template Sensors [:grey_question:](https://www.home-assistant.io/integrations/template/)
    - Sensor to show status fish feeding in a user-friendly way (sensor.template_ecogarden_fish_fed)
    - Sensor to use as argument for the Ecogarden Power Save Mode command (sensor.template_ecogarden_power_save_mode)
    - Sensor to use as argument for the Set Plant Led Brightness command (sensor.template_ecogarden_plant_led_brightness)
    
     #### Command Line Sensors [:grey_question:](https://www.home-assistant.io/integrations/sensor.command_line/)
    - Sensor to capture server response after fish feeding command (sensor.ecogarden_feedfish_result)
 
 
  - [Automations](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/automations) [:grey_question:](https://www.home-assistant.io/docs/automation/basics/)
    -     
    - Feed the fish at 9am unless already fed manually earlier (automation.ecogarden_feed_fish_at_9am)
    - Reset the 'fish already fed check' at midnight to allow automatic feeding the next day (automation.ecogarden_reset_feed_fish_check)
    - Turn Ecogarden Power Save Mode on or off (automation.ecogarden_power_save_mode)
    - Change plant led brightness when not in Ecogarden Power Save Mode (automation.ecogarden_plant_led_brightness)


  - [Scripts](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/scripts) [:grey_question:](https://www.home-assistant.io/integrations/script/)
    -
    - Feed the fish (script.ecogarden_feed_fish), which is used in the above automation and to manually trigger fish feeding via the back-office.  Script also activates the 'fish already fed check' (to avoid automatic feeding when fish already got fed manually) and checks whether the Ecogarden responded to the command.   Bassed on the result of the response check, either one of the below scripts is executed:
      - 'Success' script that updates the Feed Fish Check (script.ecogarden_feed_fish_success)
      - 'Fail' script that sends out a notification to warn about the failed fish feeding attempt (script.ecogarden_feed_fish_fail)


  - Helpers
    - 
    - Fish already fed check (input_boolean.ecogarden_fish_fed)
    - Slider to manually set the brightness of the plant led (input_number.ecogarden_plant_led_brightness)
    - Dropdown list (input_select.ecogarden_plant_led_mode) to choose between:
      - Ecogarden Power Save Mode: Plant led is managed automatically by Ecogarden itself (brightness, automatically off after 10pm, ...)
      - Local Power Save Mode: Brightness of the plant led is managed locally by taking into account the value of the abovementioned slider and the ambient light brightness + plant led turned off when not home or asleep
      - Manual: Brightness of the plant led is solely based on the value of the abovementioned slider + plant led turned off when not home or asleep

    Helpers are created in the HA back-office (Configuration > Automations & Scenes > Helpers)


  - [Template Lights](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/template_lights) [:grey_question:](https://www.home-assistant.io/integrations/light.template/)
    - 
    - Aquarium Light (light.template_aquarium) which allows to turn on/off the extra light that I put in the aquarium itself to be able to see the fish better (see "Extra's" below)
    - Plant Led (light.template_ecogarden_plant_led) which allows to turn on/off the led above the plants and to change the brightness

    I am using template lights as these are recognized 'automatically' as lights by Google Home when exposed.
  
  - [HA Back-Office](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/lovelace)
    - 
![Lovelace Card](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/lovelace_card.png)
 
 
  - Google Assistant / Google Home Integration [:grey_question:](https://www.home-assistant.io/integrations/google_assistant/)
    - 
    The below steps only work if you have already set up a working connection between your HA environment and Google Assistant.
    
    #### Fish Feeding [:movie_camera:](https://github.com/farstreet/HA_ecobloom_ecogarden/blob/main/movies/GH_fish_feeding.mov)
    - Ensure that the script 'script.ecogarden_feed_fish' is exposed within the Google Assistant settings of your HA environment (Configuration > Home Assistant Cloud > Google Assistant > Manage Entities)
    - Once exposed, the script appears as a scene under 'Home Control' in the Google Assistant app
    - Feed the fish with the command: 'Hey Google, Activate Fish Feeding'
    - Alternatively you can also create a routine that reacts to voice command 'Hey Google, Feed The Fish' and which then automatically activates the 'Activate Fish Feeding' scene.

    ![Routine Example](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/routine_example.png)

    #### Aquarium Temperature
    - Ensure that the sensor 'sensor.ecogarden_temperature' is exposed within the Google Assistant settings of your HA environment (Configuration > Home Assistant Cloud > Google Assistant > Manage Entities)
    - Once exposed, the sensor appears as a device under 'Home Control' in the Google Assistant app
    - Rename the device to 'Aquarium' in the Google Assistant App
    - Ask for the temperature using the command: 'Hey Google, what is the temperature of the aquarium?'

    ![Aquarium Temperature](https://raw.githubusercontent.com/farstreet/HA_ecobloom_ecogarden/main/images/aquarium_temperature.png)

    #### Plant Led
    - Ensure that the sensor 'light.template_ecogarden_plant_led' is exposed within the Google Assistant settings of your HA environment (Configuration > Home Assistant Cloud > Google Assistant > Manage Entities)
    - Once exposed, the sensor appears as a device under 'Home Control' in the Google Assistant app
    - Rename the device to 'Plant Led' in the Google Assistant App
    - Turn on/off the Pland Led by using the command: 'Hey Google, turn on/off the Plant Led'
    - Brightness can be changed with 'Hey Google, dim the Plant Led' or 'Hey Google, set the Plant Led to (e.g.) 50%'
    - Note that this will only work when the operation mode is set to 'Local Power Save Mode' or 'Manual'

  - Extra's
    - 
    To further enhance the experience of the Ecogarden, I'm also using the following tools, which are integrated into HA as well.
    
    - As the Ecogarden only has a led lamp above the plants but not in the aquarium itself, I've added an aquarium specific light solution myself.  To be able to automatically turn the aquarium lights on and off (based on presence, time of day, etc..), I am using a [Z-Wave](https://www.home-assistant.io/integrations/zwave_js/) Smart Switch.
    - A [template binary sensor] https://www.home-assistant.io/integrations/template/ that indicates whether someone is at home (on/off).
    - A [template binary sensor] https://www.home-assistant.io/integrations/template/ that indicates whether someone is in bed (on/off). 

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
