# Raspberry Pi 2 Autopilots

## Developer Quick Start

### OS Image

Use the Emlid RT Raspbian image till the default pre-configured PX4 image is made available. The default image will have most of the setup procedures shown below already preconfigured.

### Setting up access

The Raspbian image has SSH setup already. Username is "pi" and password is "raspberry". You can connect to your RPi2 over a network (Ethernet is set to come up as DHCP by default) and then proceed to configure WiFi access. We assume that the username and password remain at their defaults for the purpose of this guide.

<aside class="todo">
Add some wifi setup instructions
</aside>

Find the IP address of your Pi from your network, and then you can proceed to connect to it using SSH.
<div class="host-code"></div>

```sh
ssh pi@<IP-ADDRESS>
```

### Changing hostnames

To avoid conflicts with any other RPis on the network, we advise you to change the default hostname to something sensible. We used "px4ap" for our setup. Connect to the Pi via SSH and follow the below instructions.

1. Edit the hostname file

<div class="host-code"></div>

```sh
sudo nano /etc/hostname
```

Change ```raspberry``` to whatever hostname you want (one word with  limited characters apply)

CTRL+X press Y then hit Enter

2. Next you need to change the hosts file

<div class="host-code"></div>

```sh
sudo nano/etc/hosts
```
Change the entry ```127.0.1.1 raspberry```

To 127.0.1.1 <YOURNEWHOSTNAME>

If your network has DHCP setup properly, you should even be able to directly SSH without the IP address now, by insteam specifying the hostname.

<div class="host-code"></div>

```sh
ssh pi@px4ap # Our hostname here is "px4ap"
```

### Configuring a SSH Public-Key 

In order to allow the PX4 development environment to automatically push executables to your board, you need to configure passwordless access to the RPi. We use a public-key authentication method for this.

To generate new SSH keys enter the following command (Choose a sensible hostname such as <YOURNANME>@<YOURDEVICE> where we have used pi@px4ap):

<div class="host-code"></div>

```sh
ssh-keygen -t rsa -C pi@px4ap
```
Upon entering this command, you'll be asked where to save the key. We suggest you save it in the default location ($HOME/.ssh/id_rsa) by just hitting Enter.

Now you should see the files id_rsa and id_rsa.pub in your .ssh directory in your home folder:

<div class="host-code"></div>

```sh
ls ~/.ssh
authorized_keys  id_rsa  id_rsa.pub  known_hosts
```
The ```id_rsa``` file is your private key. Keep this on the development computer.
The ```id_rsa.pub``` file is your public key. This is what you put on the targets you want to connect to. 

To copy your public key to your Raspberry Pi, use the following command to append the public key to your authorized_keys file on the Pi, sending it over SSH:

<div class="host-code"></div>

```sh
cat ~/.ssh/id_rsa.pub | ssh pi@<destination_host> 'cat >> .ssh/authorized_keys'
```

Note that this time you will have to authenticate with your password ("raspberry" by default).

Now try ```ssh pi@<destination_host>``` and you should connect without a password prompt.

If you see a message ```Agent admitted failure to sign using the key.``` then add your RSA or DSA identities to the authentication agent, ssh-agent and the execute the following command:

<div class="host-code"></div>

```sh
ssh-add
```
If this did not work, delete your keys with rm ~/.ssh/id* and follow the instructions again.

### Testing file transfer
We use SCP to transfer files from the development computer to the target board over a network (WiFi or Ethernet).

To test your setup, try pushing a file from the development PC to the Pi over the network now. Make sure the Pi has network access, and you can SSH into it. 

<div class="host-code"></div>

```sh
echo "Hello" > hello.txt
scp hello.txt pi@<destination_host>:/home/pi/
rm -hello.txt
```
This should copy over a "hello.txt" file into the home folder of your RPi. Confirm that the file indeed copied, and you can proceed to the next step.

### Native builds (optional)

You can run PX4 builds directly on the Pi if you desire. This is the *native* build.
The other option is to run builds on a development computer which cross-compiles for the Pi, and pushes the PX4 executable binary directly to the Pi. This is the *cross-compiler* build, and the recommended one for developers due to speed of deployment and ease of use. For cross-compiling setups, you can skip this step.

The installation script will automatically update the native toolchain to that required by PX4.

<div class="host-code"></div>

```sh
git clone https://github.com/pixhawk/rpi2_toolchain.git
cd rpi_toolchain
./install_native
```
### Building the code 

Continue with our [standard build system installation](starting-installing-linux.md).

