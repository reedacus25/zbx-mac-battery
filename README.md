# zbx-mac-battery
Zabbix Template for Mac Peripheral Battery Levels

Simple static template for pulling battery levels for wireless peripherals on a Mac.

This is tested against a single machine, a Mac Mini M1, running Big Sur 11.5.2.

I cooked this up as a simple means to grab keyboard and trackpad battery levels so that I can know when to recharge those peripherals.

I collect the data using `ioreg` inside of MacOS
```
ioreg -r -d 1 -k BatteryPercent -a
```
This pulls the data in XML format, and I use the following XMLpath in Zabbix to pull the battery levels for each item.
```
/plist/array/dict[1]/integer[2]
```

Ideally I would like to rework this to use item discovery to automatically discover any items, and create them using the device name.
That XMLpath is:
```
/plist/array/dict[1]/string[14]
```

Right now I am just using macros at the template level to hard code what device to pull for, and assuming it will never change.
I just need to get better with discovery before implementing that.
