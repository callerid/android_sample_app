# Sample App for Android
Android Sample Caller ID Application - min API 25

## Developing using Android Studio's emulator
All CallerID.com applications that interface with Ethernet Link (EL) devices require binding to UDP port 3520. Android Studio emulators create a virtual, isolated network. 

Packets sent on port 3520 by [CallerID.com's Ethernet Emulator Deluxe ](https://callerid.com/developers.php?tab=test) will need to be re-directed to the Android Studio's emulator. This allows Caller ID packets to be seen by the sample app. This can be accomplished using a program called 'telnet'.

Follow the instructions below to launch and configure your emulator for CallerID.com testing support.

  #### Running your Emulator
  - Select the terminal tab at the bottom of Android Studio.
  - Inside the terminal type the follow:
    
    ``` 
    cd "PathToAndroidSDK\emulator"
    .\emulator.exe" -avd DeviceName -feature -Wifi
    ```
    An example of this command is as follows:
    ```
    cd "C:\Users\spenl\AppData\Local\Android\android-sdk\emulator"
    .\emulator.exe -avd Pixel -feature -Wifi 
    ```
  - The previous command will fill (prevent you from using it) the current terminal so you will need to open another terminal by clicking the plus button in the Terminal window area.
  #### Conntecting to your Android emulator
  - In order to do the next few steps you need a program called 'telnet' : follow [these instructions](https://www.technipages.com/windows-10-enable-telnet) to make sure it's installed
  - In the second terminal type:
    ```
    telnet local host 5554
    ````
    *Note: the '5554' may be different if running more than one emulator*
    
  - The above command will prompt you with the location of your Android authentication file, commonly found in: 'C:\Users\YourUsername\\.emulator_console_auth_token'
  - Open your authentication file and copy all the contents to your clipboard.
  - In your telnet terminal type 'auth' and paste your token as shown below:
    ```
    auth PastedToken
    ```
    You should see "Android Console: type 'help' for a list of commands" printed to the terminal. This means you have successfully connected to Android Studio's emulator.
  - Type the following:
    ```
    redir add udp:3520:3520
    ```
  - You have now added a redirection from your local machine into your Android Studio emulator.
  - Run the sample application

In addition to the above steps, you must choose how you will perform test calls. Below are your two options.

## With CallerID.com's Hardware Devices
  - Launch 'Emulator Redirector.exe' located at the root of this repo.
  - Confirm you have connected the CallerID.com Ethernet device
  - Perform test calls

## With CallerID.com's Ethernet Emulator
  - Open CallerID.com's Ethernet Emulator and set the IP address at the top to: ```127.0.0.1```
  - Select your format options and click Send.
  - Now you should be able to send test calls into the Sample Application without the need of a CallerID.com device.
 

# Help
If you are unable to get the UDP redirection working, refer to the [Manual: Redirection](https://developer.android.com/studio/run/emulator-networking#consoleredir)
