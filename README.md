# Helios ECx00 Pro/Vallox xx SE Plugin for smarthomeNG

Detailed documentation can be found on the Wiki: https://github.com/Tom-Bom-badil/helios/wiki


Plugin installation in short:
-----------------------------

The plugin is part of the standard smartHomeNG repository, so there is no need anymore to manually copy/paste files into the shNG plugins folder.

However, in order to get your Helios/Vallox device online, you still need to copy the following files from plugins/helios/files:

<pre>
files/helios.yaml         copy to smarthome/items
files/helios_logics.py    copy to smarthome/logics
</pre>

Then add the following lines to smarthome/etc/plugin.yaml:

<pre>
helios:
    plugin_name: helios
    tty: /dev/ttyUSB0     # put your serial port here (usually /dev/ttyUSB0 or /dev/ttyAMA0)
    cycle: 60             # update interval in seconds; ex-default: 300
</pre>

Finally add the following lines to smarthome/etc/logic.yaml:

<pre>
fanspeed_uzsu_logic:
    filename:   helios_logics.py
    watch_item: ventilation.fanspeed.fanspeed_uzsu

booster_logic:
    filename:   helios_logics.py 
    watch_item: ventilation.booster_mode.logics.switch 
</pre>

Restart smarthomeNG, the plugin should be running by now (check items for data in the Admin Interface --> Items --> Ventilation).
If no data are read out, you can find troubleshooting options at the Wiki (see above).

Fine tuning:
------------

Open smarthome/items/helios.yaml, look for the first section and adjust the specific data of your house (m², m³ etc) and your Helios/Vallox device (max air volume per hour, power levels etc). You will need to restart shNG once more to apply changes to this file.

Activating the smartVISU widget:
--------------------------------
Copy the following files found in smarthome/plugins/helios/files:

<pre>
sv_widgets/*        everything goes into smartVISU/widgets
pics/helios/*       everything goes into smartVISU/pics/helios (create dir first)
</pre>

The widget is now available within the sV. Now add following 2 lines to your HTML whereever you want to display the widget:

<pre>
{% import "helios.html" as helios %}
{{ helios.show_widget('EC300Pro', true, 'Kontrollierte Wohnraumlüftung') }}
</pre>

Meaning of the widget options:
<pre>
{% raw %}{{ helios.show_widget(id, use_uzsu, title) }}{% endraw %}
id          unique id
use_uzsu    display UZSU icon true / false
title       optional title on top
</pre>

Enjoy! :)
---------
