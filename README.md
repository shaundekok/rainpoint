# Rainpoint API Node-Red Flow
Thank you to https://github.com/Remboooo for making this possible

This Project is intended for someone with existing Home Assistant / Node-Red Experience

Requirements:
1. Home Assistant
2. Node-Red Addon, additional nodes
   - node-red-contrib-crypto-js
   - node-red-contrib-random-string
   - node-red-contrib-credentials
4. MQTT
5. Homgar Application (instead of Rainpoint):

   Logging in via this API will log you out in the app. It is advisable to create a separate API account from the app:
  - Log out from your main account
  - Create a new account
  - Log out and back into your main account
  - Invite your new account from 'Me' → 'Home management' → your home → 'Members'
  - Log out and back into your new account
  - Accept the invite
  - Make sure that you remove the default "home" that is created. Only the home with the sensors should remain in the 2nd accounts.
6. Rainpoint Device Address
   It is important that your sensor's device addresses are consecutive. Gaps in the numbering are casued when sensors are removed. I will look to implement a workaround in a future release.
  - Go through the list of sensors in the app from top to bottom.
  - Open each sensor, then click settings and review the device address.
  - The first sensor should be 1, then next 2, then 3 etc.
  - If they are not, remove the sensors that are after the gap and re-add them. This should close this gap and prevent the flow from erroring out.

Setup
1. Install the Addtional Nodes
2. Import the JSON file into your Node-Red Instance
3. Update the following Nodes:
   - Credentials (Use new account created above) 
     - areaCode: Telephone Country Code, i.e. "27"
     - phoneOrEmail: email address
     - payload: password
     - count: -1
     - Set repeat for every 1 to 3 minutes
   - MQTT Out Discovery
     - Add your MQTT Server Details, including credentials
4. Deploy this flow.
5. Make sure that the following connect:
  - MQTT Out Discovery
  - MQTT Out State
6. The values will automatically be displayed using MQTT Auto Discovery, i.e. sensor.rainpoint_"sensor name"_variable
7. The flow has been setup to sync data every 5 minutes. This is inline with the standard app syncing.

If you would like to use the Rainpoint App (instead of Homgar), you need to change the appCode to 2 in the following nodes:

- Hamgar Login
- Hamgar Get Home
- Hamgar Devices
- Hamgar Get Device Status

Dashboard

<img width="1411" height="649" alt="image" src="https://github.com/user-attachments/assets/e1630b3f-f1bb-4521-9b38-1d6c730c9a18" />


Supported Devices:
1. RainPoint Smart+ Soil & Moisture Sensor (HCS021FRF) - New Decoder
2. RainPoint Smart+ High Precision Rain Sensor (HCS012ARF) - New Decoder
3. RainPoint Smart+ Water Flow Meter (HCS008FRF) - New Decoder
4. RainPoint Smart+ Air Quality Meter (HCS0530THO) | CO₂ Detector | Temp | Humidity - New Decoder
5. RainPoint Smart+ Temperature, Humidity & Lux Sensor (HCS014ARF) - New Decoder
6. RainPoint Smart+ Temperature & Humidity (HCS026FRF) - New Decoder
7. RainPoint Smart+ Smart Pool Thermometer (HCS0528ARF) - Coming Soon
