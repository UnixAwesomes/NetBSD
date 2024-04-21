## About
Today we will look at how to connect Bluetooth headphones on NetBSD.

## Bluetooth start

Enable Bluetooth operation on the system in this way:

Add the following line to /etc/rc.conf.

`bluetooth=YES`

Start the bluetooth service.

`/etc/rc.d/bluetooth start`

## Device pairing

To start searching for devices, type the command

`btconfig ubt0 inquiry`

After that you should see your device in the list The device ID should look something like this
`1: bdaddr XX:YY:ZZ:XX:YY:ZZ`.

For easy device pairing, add an inscription to /etc/bluetooth

`echo "XX:YY:ZZ:XX:YY:ZZ headphones" >>/etc/bluetooth/hosts`

After that, start pairing

`btpin -d ubt0 -a headphones -p 0000`

## Sound customization

To make the sound work, enter

`bta2dpd -a headphones /dev/pad`

Then run the `audiocfg list` command, and find Bluetooth audio in the list

Select Bluetooth Audio by default with the command

`audiocfg default ID`
