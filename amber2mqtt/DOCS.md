# Home Assistant Add-on: Amber2MQTT

This addon will based on the timing schedules you setup:
1. Poll the Amber API using your account details
2. Poll the AEMO website to retrieve the latest actual price & data for the current interval

**NOTE:** This Add-on does require a MQTT Broker, you can use the Mosquitto Add-on or an external Broker

## Installation
To install this add-on is similar to any other HA Add-on after you have added this repository to the Add-on Store
1. Navigate to the Add-on Store page
2. Click on the 3 dots at the top Right corner and select Repositories
3. Add the URL "https://github.com/cabberley/amber2mqtt-addon" click add and then close.

A refresh of your Store page should now display the Amber2MQTT Add-on

4. Click and open the Amber2MQTT add-on and click on install. This will start the process of downloading and setting up the Add-on

After it has downloaded, you will need to then edit the configuration for the Add-on

### Basic Configuration

5. Open the Add-on and change to the Configuration tab across the top of the screen.
6. In the Amber section add your Amber Site_id & access_token. (You can get them from the Amber Website)
7. In the MQTT section at the bottom enter the details for your mqtt Broker.
   If you are using the Mosquitto Add-on
   1. The username and password can be any of your HA Users
   2. The broker will be the IP Address of your Home Assistant server
  
### Advanced Configuration

In the Amber and AEMO sections there are a pair of keys for seconds and minutes. These instruct the scheduling engine inside the Add-on what time periods to poll the Amber and AEMO sites respectively.
In the default config for example the Amber Site will be polled:
 - on each listed second "14,16,18,19,21,23,25,27,30,32,35,40,45,50,55"
 - When the Minute equals "0-1,5-6,10-11,15-16,20-21,25-26,30-31,35-36,40-41,45-46,50-51,55-56"
 - When the code gets a confirmed price for the current 5 minute interval it will then stop and not continue until the next 5 minute interval starts.

Amber limits you currently to 50 requests per 5 minutes and if you exceed that you will be blocked until the next 5 minute period starts. So also take into considderation what other apps you have that are also hitting the Amber website as you will quickly run out of calls if there are delays in the price being published.

