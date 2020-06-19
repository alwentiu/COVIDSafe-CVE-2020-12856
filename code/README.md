# Silent Pairing Issue Proof-of-Concept

This proof-of-concept (PoC) code shows how to trigger the silent pairing in Android, when an app makes a GATT connection, as a central, to a peripheral and reads a characteristic. What the code does is basically creates a GATT server, with an encrypted and authenticated characteristic with an UUID that matches the UUID the client app is connecting to. 

## System requirements

This PoC has been tested in a desktop running Ubuntu 18.04 LTS, running the bluez bluetooth stack implementation. You will need to install the python-dbus package if you haven't already installed it:

> sudo apt install python-dbus


## Testing the PoC

1. Run the setup.sh script
 > sudo ./setup.sh

2. Run exploit1.py to advertise a GATT service. The service UUID is '12345567-1595-4f6a-80f0-fe094cc218f9'.

 > sudo python3 exploit1.py

3. Use any bluetooth debugger app to connect to the GATT server advertised in step 2. We used the nRF Mobile Connect app (the Android version) in our test. 

4. Read the characteristics in the GATT server. This will cause the phone to be bonded to the server silently, without prompting the user. 

5. After the bonding finishes, the IRK of the phone and other details can be found in /var/lib/bluetooth in the desktop. 

Optionally, you can use a bluetooth monitor to see the detailed exchanges between the desktop and the phone. We used Wireshark in our tests.

 
