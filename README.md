# How to stop the DHCP server on the Vodafone Station Revolution

I recently moved from a FTTC contract to a FTTH one with Vodafone. For the upgrade Vodafone sent me the new Vodafone Wifi 6 Station. 

Since I still had the previous Vodafone Station Revolution lying around I wanted to use it as an Access Point to increase the range of the Wifi.

In my firmware (5.4.8.1.406) on the VSR there is the possibility to switch mode for the VSR into a "Generic modem" which sounded great.

However, in the WebGUI there is no way to turn off the DHCP server or the gateway address of the VSR and this was causing confilcts in the net.

Luckily there is an amazing [italian forum](https://www.hwupgrade.it/forum/showthread.php?t=2729821) with tons of information about the VSR. 
From few posts, I discovered that, after authentication, is possible to directly send commands to the backend of the VSR (even for those not present in the GUI) via the browser console.

In the forum I couldn't find the command I needed so I digged a bit into the javascript code in the VSR and found the right command. 
I'm sharing here the procedure in case it could be useful for someone else.

## How to

1) Go to the managment page of your VSR (usually https://192.168.1.1/) and log in with your password
   ![image](https://github.com/marcoavesani/stop_dhcp_vodafone_station_revolution/assets/3177391/c3e00228-38bd-44e9-a464-aa0ccc3cab52)
2) Open the console. In chrome, for example, you just need to right click on the webpage and select "Inspect". On the top right of the newly opened window select Console.
   ![image](https://github.com/marcoavesani/stop_dhcp_vodafone_station_revolution/assets/3177391/8dc527d3-d1c3-40e7-ba87-af80a61562f0)
3) Paste the following line in the console:
   ```
    send_value('InternetGatewayDevice.X_JUNGO_COM_TR_181.Device.DHCPv4.Server.Pool.3.Enable', false, function(x){console.log(new XMLSerializer().serializeToString(x))});
    ```
![image](https://github.com/marcoavesani/stop_dhcp_vodafone_station_revolution/assets/3177391/f5009288-dda5-46c6-9d2a-b46740dc6873)

4) That's it! To check that the DHCP server is off in the status page
   
   ![image](https://github.com/marcoavesani/stop_dhcp_vodafone_station_revolution/assets/3177391/9fd07ab7-8ca3-4f66-81da-5d60b46640cb)

## Other commands
If you need to change other parameters not available in the webgui try checking the [forum](https://www.hwupgrade.it/forum/showthread.php?t=2729821), the javascript sources in the VSR or by downloading the backup configuration file in XML from your VSR.
