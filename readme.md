# RemoteRelativeInput
## About This Program
This program is designed to allow relative input in an RDP (VNC) session by wrapping an existing remote desktop client window with another window and sending the client's input information using an SSH session. Currently, only sessions from a Windows machine to a Windows or Linux machine are supported.

![sample](https://gyazo.com/5b6e57408136ba4fcebfd2525b7dc232.gif)


## News 

If you are going to use this for connecting from Windows to Windows via RDP (RemoteDesktop), RDPRelativeInput is available!

Check: 
[github.com/TKMAX777/RDPRelativeInput](https://github.com/TKMAX777/RDPRelativeInput)


## install

### Server

#### Debian / Ubuntu

```sh
sudo apt install xdotool golang-go
go install github.com/TKMAX777/RemoteRelativeInput/cmd/RelativeInputServer@latest
```

#### Windows

1. The [Go](https://go.dev/doc/install) and [OpenSSH Server](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) must be installed before installation.
2. Run the following commands on CMD.

```cmd
go install github.com/TKMAX777/RemoteRelativeInput/cmd/RelativeInputServer@latest
go install github.com/TKMAX777/RemoteRelativeInput/cmd/RelativeInputWorker@latest
```

  ☆ Windows requires a separate worker program to send messages to the user session.
  
### Client

1. The [Go](https://go.dev/doc/install) and [OpenSSH Client](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) must be installed before installation.
2. Run the following commands on CMD.

```sh
go install github.com/TKMAX777/RemoteRelativeInput/cmd/RelativeInputClient@latest
```

## Usage

### Connect to Windows

1. Open Remote Desktop Connection and connect to your server like usual and have it in Maximize Windowed (**NOT FULL SCREEN**)
2. Open cmd and start the worker program on the host machine.

```
start /d "C:\Users\<HostFolderName>\go\bin" RelativeInputWorker.exe
```

  ☆ replace &lt;HostFolderName&gt; with the name of the folder of your account located in `C:\Users`

3. Starts a SSH session from the client machine on cmd.

```
set CLIENT_NAME=<HostAddress> - Remote Desktop Connection
RelativeInputClient.exe | ssh <HostUsername>@<HostAddress> "C:\Users\<HostFolderName>\go\bin\RelativeInputServer.exe"
```

  ☆ replace &lt;HostFolderName&gt; with the name of the folder of your account located in C:\Users<br />
  ☆ replace &lt;HostUsername&gt; with the Host username<br />
  ☆ replace &lt;HostAddress&gt; with the IP of your host<br />
  ☆ It is reported that it does not work properly in PowerShell.<br>

4. Ignore the message box and click on cmd tab, and enter host user password

5. Press Yes in the message box displayed on the host machine.

6. Press OK in the message box displayed on the client machine.

7. Enjoy!

  ☆ The mouse cursor disappears during relative input mode. If you need the cursor, use the F8 key to switch to absolute input.<br />
  ☆ To return to relative input mode, select the RDP Input Wrapper window and hit the F8 key again.<br />
   
### Connect to Debian / Ubuntu

```sh
set CLIENT_NAME=<hostname> - Remote Desktop Connection
RelativeInputClient.exe | ssh <hostname> /home/<UserName>/go/bin/RelativeInputServer
```

  ☆ The mouse cursor disappears during relative input mode. If you need the cursor, use the F8 key to switch to absolute input.<br />
  ☆ To return to relative input mode, select the RDP Input Wrapper window and hit the F8 key again.<br />
  ☆ replace &lt;HostFolderName&gt; with the name of the folder of your account located in `C:\Users`

## Copyright

Copyright 2022- tkmax777 and contributors
