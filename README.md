# Aluvation-Model-Demo
Model of an Aluvation container. LED color change triggered by the luminisoty sensor of the provisioned XDK.

## Introduction
The model is based on the product offer from Aluvation: Mobile micro-factories contained in standard containers. With the help from relayr, Aluvation is able to offer heat treatment as a service: Connecting treatment plants allows to obtain insights about health, proper usage, consumption, as well as machine lifetime and allows for billing integration for as a Service Models.
The model allows to manually roll in and out a platform, simulating the conveyor belts that feed the heat treatment micro factory. An XDK painted in silver simbolises the Aluminum pieces which are treated by the micro-factory. The XDK light sensor is used to detect if the product is inside, or outside the container and triggers the color of the LED lights within and below the container model: Blue when the XDK is outside the container and red when it is inside.  

## Smart Light Set-Up
1.	Install the LIFX app in your phone.
2.	Login with the following credentials:
marketing@relayr.io
Password: 10LeUT2MKdcxCNq5TxfS
3.	Connect with your phone to the hotspot where you wish to connect your Light to.
(This step is important: For set-up, the mobile phone and the lights need to be connected to the same hotspot) 
4.	Connect Stripes to power connector. Make sure all the necessary stripes are connected. (It is not possible to add a stripe length otherwise).
5.	Connect power connector to the outlet.
6.	Reset Stripe by pressing the reset button for a longer time, until the stripe starts to change colors in a loop.
7.	Open wifi setup in Cell Phone
Below the available hotspots a new option will appear:
“SET UP NEW DEVICE”
Choose the LIFX Z Stripe (i.e LIFX Z 27202D)
Here you have a chance to name the stripe however you prefer to
8.	App will offer the option to connect to the hotspot the cell Phone is connected to.
Click “YES”
No password will be required since you are already connected to the Hotspot.
The following confirmation should appear in your phone:
“This accessory joined “XXX-Hotspot”
9.	Open the LIFX app in your phone
The stripe you just added should appear in your dashboard. Now you can turn it on and off and adjust the colors.
10.	Add lights to cloud when prompted.
Once the light is in the cloud, you may access the App in your mobile phone using any hotspot!
11.	Add the SECOND light to the app 
12.	First select the hotspot where you wish to connect the second light to in your mobile phone. 
13.	Press the “+” sign on the top right corner of the screen to add a new light.
Follow the same steps, starting with Step Nr.  4
Make sure at the end to add the light to the cloud by pressing on the name of the new light and selecting “Connect to the cloud”

During the process, if requested update the software and push it into the lights.
App will prompt: “asked light to download SW”, “Software downloading, when complete light will restart” and finally “Restart successful”.
If the update is interrupted, start it one more time and follow the instructions.

### Make sure all the lights are accessible by the LIFX API
In a browser go to: 
https://api.developer.lifx.com/docs/list-lights
(Previously login with the login and password provided in step 2).
At the end of the web site type “all” into the “Selector” field and try the command out.
Both lights should be listed as shown in the example below:

```
[
    {
        "id": "d073d52746cd",
        "uuid": "027f2dc5-cb3e-44a6-b11d-910c0e0a7f9e",
        "label": "Stripe 02",
        LIFX Z
        S/N: D073D52746CD
        CODE in Box: 258-43-678
…
…
        "id": "d073d527202d",
        "uuid": "02f7b256-f81c-4976-9997-6884e90fd644",
        "label": "Stripe 01",
        LIFX Z
        S/N: D073D527202D
        CODE in Box: 834-49-731
…
…
     }
]
```

These identifiers are important to address each specific light with your code!
All the necessary commands can be applied as indicated in the LIFX website.

The following Tokens have been requested at LIFX and are available for the demo:

```
Token01: c7d984170d4c3fd13eeda804cbc957344354a84a96b6f80eaf1b41b7d2c53b68
Token02: ce7ba337651eaac43e57cfb56b70e07602e0432f54d035195e602ad61fae0ec4
```

## XDK Set-Up
You will need:
1.	Micro SD Card Adapter
2.	Program to edit the configuration file (i.e. Sublime Text, https://www.sublimetext.com/)

XDK has been set-up to operate in Cloud 2.0
Hotspt login and password can be updated by making the necessary changes in the XDK.cfg file stored in the Micro-SD Card.

This is a sample of the XDK.cfg code:

```
MQTT_SERVER_PORT=8883
WLAN_CONNECT_WPA_SSID=relayr
WLAN_CONNECT_WPA_PASS=!D1g1t@lTransformati0n!
DEVICE_ID=f4490f54-1543-4afc-9862-8dabc1e9f5da // DEVICE_ID
MQTT_USER=f4490f54-1543-4afc-9862-8dabc1e9f5da // = DEVICE_ID
MQTT_PASSWORD=xxxxxxxxxxxxxxxxxxxxxxxxxxx 
MQTT_CLIENTID=None // only needed with cloud 1.0
MQTT_TOPIC=devices/f4490f54-1543-4afc-9862-8dabc1e9f5da/measurements // devices/DEVICE_ID/measurements
MQTT_SERVER=cloud-mqtt.relayr.io // or mqtt.relayr.io if cloud 1.0
MQTT_SUBSCRIBE=FALSE //TRUE if cloud 1.0 or FALSE if cloud 2.0
```

Do not forget to save your changes before ejecting the min SD-Card

Carefuly insert the SD Card in the XDK, otherwise it may “fall” into the XDK and you will need a screw driver to open it! Copper contacts on the top!

After turning on the XDK, the second orange light should start blinking with a regular frequency. This means the XDK is already connected to the internet via the hotspot, and it is sending already the data measured at the XDK.

The following Devices have been created for each XDK:

```
  "id": "deda1b74-3c9d-4ed2-8609-8ac21b5a58ba",
  "password": "wuGUwJ7Y0VPNmHbiNEViyugn6"
  "name": " XDK-Aluvation-Demo-01",
  "orgId": "37e94ef9-d687-47b0-99c3-09fceef76d17",
  "modelId": "bd4df8e7-08c3-4905-aa53-821eefa60402",
  "modelVersion": 2

  "id": "8ca8c942-a46f-4958-b833-882aa657f106",
  "password": "7b5ZrpYE1utpKO9DnAg4Fb6fx"
  "name": "XDK-Aluvation-Demo-02",
  "orgId": "37e94ef9-d687-47b0-99c3-09fceef76d17",
  "modelId": "bd4df8e7-08c3-4905-aa53-821eefa60402",
  "modelVersion": 2
```

## Rules
The following two rules have been set-up:

Hannover-Messe-001,
UUID: ebcd6772-e2b8-4ee5-87b5-42257bc46acb

Hannover-Messe-002,
UUID: 185e2145-a32a-4c0a-b6d1-b5ab05a4a34a	

Here you can find the original code for the Hannover-Messe-002 Rule:

```
rule.on('measurement', function(measurement) {

               if(measurement.name === 'luminosity') {
                   
                      var brightness = measurement.value
                      var alertStatus = context.get('max_temp');
                      
                if (brightness >= 500 && !alertStatus) {
                    
                  context.set('max_temp', true)
                  debug('ALERT SENT - EVENT TRIGGERED');
                  
                  var body = {"power":"on","color":"blue", "duration":4, "brightness":1};

                  var body3 = {"color":"orange","from_color":"red","period":"1","cycles":5,"persist":true,"power_on":true,"peak":0.2};

                    var headers = {
                          "Authorization" : "Bearer ce7ba337651eaac43e57cfb56b70e07602e0432f54d035195e602ad61fae0ec4"};
                    
                    actions.callHttp({
                          url: 'https://api.lifx.com/v1/lights/d073d52746cd/state',
                          method: 'PUT',
                          contentType: 'application/json',
                          headers: headers,
                          requestBody: JSON.stringify(body)
                    });

                    /*actions.sendEmail({
                          to: ["andreas.weber@relayr.io"],
                          subject: 'TEMPERATURE ALERT at Hannover Messe Oven 02',
                          message: 'Temperature in Hannover Messe Oven 02 has exceeded maximum allowed!'
                    });*/
                  
                } else if (brightness < 500 && alertStatus) {
                    
                  context.set('max_temp', false);
                  debug('ALERT CLEAR - EVENT TRIGGERED');
                  
                  var body1 = {"power":"on","color":"red","duration":4,"brightness":1};

                    var headers1 = {
                          "Authorization" : "Bearer ce7ba337651eaac43e57cfb56b70e07602e0432f54d035195e602ad61fae0ec4"};
                    
                    actions.callHttp({
                          url: 'https://api.lifx.com/v1/lights/d073d52746cd/state',
                          method: 'PUT',
                          contentType: 'application/json',
                          headers: headers1,
                          requestBody: JSON.stringify(body1)
                    });
                  
                } else if (alertStatus) {

                    debug('Third State');

                } else {
                  debug('4th State');
                  !alertStatus;
                }
                
                   
            }
});
```
## Credits
created by Andreas Weber and Michael O'Malley<br>
Based on the light sensing rule by [Andy Ryan](mailto:andy.ryan@relayr.io)

date: April 2018
