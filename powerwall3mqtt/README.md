# powerwall3mqtt
A simple Home Assistant Add On that acts as a bridge between the Powerwall 3 TEDAPI and MQTT.

## Current state
- Right now the bridge can deal with a single group of one or more Powerwall 3s.  It might also support expansion units, but I have none to test with.
- I think there's a race condition on startup, where HA doesn't see the updated states until the second publish after this starts.
- Power reporting is working for the following:
	- Aggregates of the entire system
	- Individual strings on each PW3
- Energy storage reporting is working for the following:
	- Aggregate of all batteries
	- Individual Powerwall battery levels
	- Calculations of percentage remaining and user defined backup reserve mirror the Tesla app
- No other energy reporting
	- Pypowerwall doesn't have it yet
	- Once this add on is working and officially released, this is the next thing I'll be researching
- No interactivity support
	- Can't tell the system to go Off-Grid
	- Can't change settings on the Powerwall
	- I'm planning to work on these later this year when I'm on-site where my PW3 install is

## Pre-reqs
Connecting directly to the TEDAPI requires communicating with an internal IP on the Powerwall 3 (PW3).  To make this work, you need to add a static route to 192.168.91.1 pointed at the IP of the PW3 Leader on your network.
-  If you have a segmented network you should add the route on your router.
-  If the PW3 is on the same network segment as Home Assistant, you'll need to add a static route on the Home Assistant server.  You can do that by using the [Static Route Manager add-on](../staticroutes).  For example, if the IP of your PW3 is "192.168.1.151", would would add the following to the Static Route Manager config:
```
- nexthop: 192.168.1.151
  network: 192.168.91.1/32
```

## Reporting problems
- Please switch the Logging Level to DEBUG in Configuration and restart the add-on.
	- You may need to toggle "Show unused optional configuration options" on.
- Open an issue at https://github.com/slyglif/haos-addons/issues
	- Describe the issue you are encountering
	- Include the version of the add-on
	- Include the logs
		- Include the full logs if possible
		- If the full logs are megabytes in size, at least the first 20 lines at startup and the 10 lines prior to the error
		- If including the logs inline, please quote them between "\`\`\`" marks (3 backticks)