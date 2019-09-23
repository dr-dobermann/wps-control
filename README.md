# WPS-Control

## Water pump station control

WPS-controller (WPSC) should check water leakage, water tank level, water pressure after the pump and the AC presence.
In case of unexpected events, such as power loss, water leak detection, water pressure is too low, tank water level is too high or too low, the pump should be turned off and inlet water pipe is closed by a 5-wired 12V valve.

WPSC displays its status over an 1604 I2C display. 
WPSC is controlled locally by a single button over the WPSC on-screen menu.
WPSC publishes its status updates over WIFI to a MQTT server on **"/home/facilities/wpsc"** topic (here and after "status_topic").
WPSC subscribed to an MQTT topic **"/home/facilities/wpsc/ctl"** (here and after "ctl_topic") and processed comands from it. The commands are listed below:

| Command | Description |
|---------|--------------|
| status | Shows current WPSC status on "status_topic" |
| stop   | Stops the pumps, closes inlet water pipe |
| start  | Starts (if possible) pump and opens water inlet pipe |

WPSC statuses are send as string with param=value pairs separated by a semicolon. Every param has a set of values described in a followed table.

| Parameter | Value | Description |
|-----------|-------|-------------|
| ctl       | ok</br> | WPSC is OK</br> |
|           | alarm</br> | WPSC encountered an error</br> |
|           | off   | WPSC is stopped |
| power     | ok</br> | AC power is OK</br> |
|           | off     | AC power is OFF |
| wleak     | no</br> | There is no water leak detected</br> |
|           | yes     | There is a water leak |
| wpress    | err</br>| Water press measurement error</br> |
|           | **float_num** | Water pressure in megapascals |
| wlevel    | empty</br> | Tank level too small</br> |
|           | **float_num** | Water level level</br> |
|           | full    | Water level too high |
| pump      | on</br> | Pump is on</br> |
|           | off     | Pump is off |
| inlet     | open</br>    | Inlet valve is open</br> |
|           | opening</br> | Inlet valve is opening</br> |
|           | closed</br>  | Inlet valvle is closed</br> |
|           | closing</br> | Inlet valve is closing |
