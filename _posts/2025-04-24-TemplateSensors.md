---
title: Home Assistant Template Sensor Helpers
date: 2025-04-24
categories: [Home Assistant]
tags: [homeassistant, helpers]     # TAG names should always be lowercase
---

I recently saw a ![Reddit post](https://www.reddit.com/r/homeassistant/comments/1k6p6lg/ha_helpers/) about Home Assistant helpers and wanting to leverge them more in their instance.  As someone who is always looking for interesting ways to solve problems in Home Assistant, helpers are large part of my setup.  While helpers can solve a myriad of problems, I use input boolean, binary sensor and template sensor the most.  Template helpers specifically have several other types within this sub-category.

One example of this template usage is counting items like total number of locks secured or total number of lights on. 

### Door Status Tracking Example

#### Template Sensor Code
{% raw %}
```yaml
{% set locks = [
   states.lock.entryway_lock,
   states.lock.connected_keypad_with_lever,
   states.lock.garage_lock,
   states.lock.touchscreen_deadbolt_z_wave_plus,
   ] %}
{{ locks | selectattr('state','eq','unlocked') | list | count }}
```
{% endraw %}
This same approach could be applied to several other device types. 
 
Once the template is populated with entities, and the total count is established, you can then easily use this value to apply logic to determine the status of a group of items.

I am again using templating, but this time in a card.  I prefer the look and features of mushroom card, but these same approaches can be used with other template card types.  

> Slight formatting tweaks might be needed for standard card types. 
{: .prompt-info }

The template card will look at the entity template sensor value and if, elif, else logic to set text values, icon values, and icon color.

> If you are combining items like I am between doors, covers, and locks, remember that this is getting applied top down, so make sure you are ordering items be importance.
{: .prompt-warning }

Additionally I am using card mod to change the card background if the door value is > 0

#### Mushroom Template Door Card Code:
{% raw %}
```
      - type: custom:mushroom-template-card
        primary: Locks
        secondary: |-
          {% if states('sensor.doors_unsecured_total')|int(0) > 0 %}
            Door Unsecured
          {% elif states('sensor.covers_unsecured_total')|int(0) > 0 %}
            Garage Door Unsecured
          {% elif states('sensor.locks_unsecured_total')|int(0) > 0 %}
            Lock Unsecured
          {% else %}
            All Secured
          {% endif %}
        icon: |-
          {% if states('sensor.doors_unsecured_total')|int(0) > 0 %}
            mdi:door-open
          {% elif states('sensor.covers_unsecured_total')|int(0) > 0 %}
            mdi:garage-open
          {% elif states('sensor.locks_unsecured_total')|int(0) > 0 %}
            mdi:lock-off
          {% else %}
            mdi:lock
          {% endif %}
        hold_action:
          action: none
        double_tap_action:
          action: none
        tap_action:
          action: navigate
          navigation_path: /lovelace-locks
        icon_color: |-
          {% if states('sensor.doors_unsecured_total')|int(0) > 0 %}
            red
          {% elif states('sensor.covers_unsecured_total')|int(0) > 0 %}
            red
          {% elif states('sensor.locks_unsecured_total')|int(0) > 0 %}
            yellow
          {% else %}
            green
          {% endif %}
        badge_icon: ""
        badge_color: ""
        layout: vertical
        card_mod:
          style: |
            {% if states('sensor.doors_unsecured_total')|int(0) > 0 %}
            ha-card {--ha-card-background: #4c5c92} 
            {% else %}
            {% endif %}
```
{% endraw %}
If all works well, this is how things look on the dashboard.

#### Card Door Status Screenshots

> All Doors, Covers, and Locks Secured
>
> ![All Secured](https://github.com/user-attachments/assets/5a5da5c6-42ec-41e0-b5f0-e5335adccd7a)

> Door Unsecured
>
> ![Door Unsecured](https://github.com/user-attachments/assets/42a829d2-04c9-45d7-bd17-7952368c40fa)

> Cover Unsecured
>
> ![Cover Unsecured](https://github.com/user-attachments/assets/7856b505-e171-4bc3-8669-f56e275d606d)

 

### Light Status Tracking Example

Another option would tracking lights on in your house.  I use badge icons for this setup, as it can provide a count of lights on up to a certain level as well. This one uses a combination with a helper group for outside lights as I like to know they are on at night with everthing else off, but I don't really care about the count per se. 

#### Mushroom Template Light Card Code:
{% raw %}
```
- type: custom:mushroom-template-card
        primary: Lights
        secondary: |-
          {% if states('sensor.lights_on_total')|int(0) > 1 %}
            Inside Lights On
          {% elif states('sensor.lights_on_total')|int(0) > 0 %}
            Inside Light on
          {% elif is_state("switch.outside_lights_ha", "on") %}
            Outside Lights on
          {% else %}
            All Lights Off
          {% endif %}
        icon: |-
          {% if states('sensor.lights_on_total')|int(0) > 1 %}
            mdi:lightbulb-on
          {% elif is_state("switch.outside_lights_ha", "on") %}
            mdi:lightbulb-on
          {% else %}
            mdi:lightbulb
          {% endif %}
        hold_action:
          action: none
        double_tap_action:
          action: none
        tap_action:
          action: navigate
          navigation_path: /lovelace-graphs/lights
        icon_color: |-
          {% if states('sensor.lights_on_total')|int(0) > 0 %}
            purple
          {% elif is_state("switch.outside_lights_ha", "on") %}
            blue
          {% else %}
            green
          {% endif %}
        badge_icon: |-
          {% if states('sensor.lights_on_total')|int(0) < 1 %}

          {% elif states('sensor.lights_on_total')|int(0) > 9 %}
            mdi:numeric-9-plus
          {% elif states('sensor.lights_on_total')|int(0) < 9 %}
            mdi:numeric-{{ states('sensor.lights_on_total') }}
          {% else %}

          {% endif %}
        badge_color: |-
          {% if states('sensor.lights_on_total')|int(0) > 0 %}
            red
          {% else %}
            
          {% endif %}
        layout: vertical
        card_mod:
          style: |
            {% if states('sensor.lights_on_total')|int(0) > 1 %}
            ha-card {--ha-card-background: #4c5c92} 
            {% else %}
            {% endif %}
```
{% endraw %}
#### Card Light Status Screenshots

> All Lights Off
> 
>![All Lights Off](https://github.com/user-attachments/assets/be7f01fe-21e1-4f82-a53a-1ec5fd94b370)

> One Light On
> 
>![One Light On](https://github.com/user-attachments/assets/b64c7570-0888-4304-9de3-db504f0f4616)

