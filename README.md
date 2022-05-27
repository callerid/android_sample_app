# Sample App for Android
Android Sample Caller ID Application - min API 25

### Development without Android Hardware (using Android Studio emulator)
All CallerID.com applications that interface with EL(Ethernet Link) devices require binding to UDP port 3520. This sample application will bind appropriately, but out-of-box, when using [CallerID.com's Ethernet Emulator Deluxe ](https://callerid.com/developers.php?tab=test), will not work. This is because the Android Studio emulators create a virtual, isolated network in which they access. This isolation means the Ethernet Emulator Deluxe will send out a UDP packet but the packet will not be able to pass through into the Android Studio emulator. In order to allow this passthrough, the following steps are required:

  #### Running your Emulator
  - At the bottom of Android Studio there is a terminal tab, select it.
  - Inside the terminal type the follow:
    
    ``` 
    cd "<path-to-sdk>\emulator"
    .\emulator.exe" -avd <name-of-your-device> -feature -Wifi
    ```
    An example of this command is as follows:
    ```
    cd "C:\Users\spenl\AppData\Local\Android\android-sdk\emulator"
    .\emulator.exe -avd Pixel -feature -Wifi 
    ```
  - That command will fill the current terminal, at the top of the terminal window click the plus to open another terminal.
  - In order to do the next few steps you need a program called 'telnet' : follow [these instructions](https://www.technipages.com/windows-10-enable-telnet) to make sure it's installed
  - In the second terminal type:
    ```
    telnet local host 5554
    ````
    *Note: the '5554' may be different if running more than one emulator*
  - The above command will prompt you with the location of your Android authentication file, commonly found in: 'C:\Users\ YOUR_USERNAME \.emulator_console_auth_token'
  - Open your auth. file and copy all the contents to your clipboard.
  - In your telnet terminal type:
    ```
    auth pasted-token
    ```
    You should see "Android Console: type 'help' for a list of commands" printed out. If so, you've logged in
  - Next type the following:
    ```
    redir add udp:3520:3520
    ```
  - You have now added a redirection from your local machine into your Android Studio emulator.
  - Run the sample application
  - Open CallerID.com's Ethernet Emulator and set the IP address at the top to: ```127.0.0.1```

You should be able to send test calls into an emulated UDP port 3520 networked application now.



# Help
If you are unable to get the UDP redirection working, refer to the [Manual: Redirection](https://developer.android.com/studio/run/emulator-networking#consoleredir)
