---
layout: post
title: Home Assistant Lovelace Custom Cards How-to
subtitle: Reset on Click Day Counter Reminder Cards How To
tags: [archive, reddit, guide]
comments: true
author: Dani
---

This is an excerpt from [this reddit post](https://www.reddit.com/r/homeassistant/comments/1hdv07e/reset_on_click_day_counter_reminder_cards/) I made from my now deleted account 

Each Bubble Needs:
 
[A Date Time Helper](https://www.home-assistant.io/integrations/input_datetime/)
[An Automation to allow resetting](https://www.home-assistant.io/integrations/input_datetime/#actions)
[The actual Lovelace Display card](https://github.com/piitaya/lovelace-mushroom/blob/main/docs/cards/chips.md)

Making the Helpers: Navigate to the helper GUI configurator

    /config/helpers

Select Date and/or Time from the helper creation window [CreationWindow](https://i.imgur.com/Fw4Lkz1.png)

Give it a name and choose a fun icon

(note the icon string after selection you will need it for later)

Next setup the reset Automation

This automation simply sets the date-time helper to the current time whenever it is fired.

```
alias: New Reminder Reset
description: ""
triggers: []
conditions: []
actions:
  - action: input_datetime.set_datetime
    metadata: {}
    data:
      datetime: "{{ now().timestamp() | timestamp_local }}"
    target:
      entity_id: input_datetime.new_reminder
mode: single
```

There are a few ways to accomplish this but this code block will allow the reset to be timezone agnostic (using the system-configured timezone) just remember to set the entity_id to the helper you named and created earlier

Note: Metadata might not be needed

[Lastly let's make the card for lovelace I used Mushroom Chips Card](https://github.com/piitaya/lovelace-mushroom/blob/main/docs/cards/chips.md)
But realistically you could use whatever you want

Select Template from the drop-down in the GUI configurator [GUI configurator](https://i.imgur.com/ieDGUyy.png)

Input your icon string from earlier [Icon String](https://i.imgur.com/DpDZOEd.png)

After that, we'll configure the counter and reset functions. ![CounterReset](https://i.imgur.com/VydTrBe.png)
{% raw %}
```
{{(((as_timestamp(now())-states.input_datetime.new_reminder.attributes.timestamp)) | int /60/1440) | round(1)}} Days Since Reminder Reset
```
{% endraw %}
You can simply copy paste the above block into content and change "new_reminder" to the name of your helper, give it some flavor text, in this instance "Days Since Reminder Reset" can be changed to say anything, and then under the automation target choose your reset automation from the entity list

a quick explanation of what is happening here so you can further customize it

```
as_timestamp(now())
```

provides the current time in a format we can do math with

we then subtract that from the time saved within the helper which is accessed using
```
states.input_datetime.new_reminder.attributes.timestamp
```
we then convert that timestamp into days and round it to the nearest tenth of a day
```
| int /60/1440) | round(1)
```
Additionally this specific card allows setting the colour of the icon and it can be done conditionally too.

IE. it is possible to change the icon's colour as it progress so if say you want the icon to be Yellow if it's been too many days
{% raw %}
```
{{'#F3A83C' if (((as_timestamp(now())-states.input_datetime.litter_box_cabinet_door_openattributes.timestamp))| int /60/1440) | round(1) >= 3}}
  ```
  {% endraw %}