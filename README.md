Hi All,<br><br>
I thought I'd upload what I have been working on recently on Home Assistant ! Hopefully it gives you an idea of what I've done and how you can use it yourself if interested.
<br>
<br>

# Theme

Based on the work done here by LE0N: [https://community.home-assistant.io/t/rounded-dashboard-guide/543043](https://community.home-assistant.io/t/rounded-dashboard-guide/543043)
<br>

My altered and modified theme can be found here: [rounded-alt-2.yaml](https://github.com/beecho01/homeassistant-setup/blob/main/themes/rounded/rounded-alt-2.yaml)

<br>

# Dashboard

<details>
<summary>GUI Setup</summary>

<br>

```
views:
  - title: Home
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:button-card
            show_name: true
            show_label: true
            show_icon: false
            show_state: false
            name: |
              [[[
                const hour = new Date().getHours();
                let greeting;
                if (hour >= 18) {
                  greeting = ["Good evening", "Evening", "Welcome back", "Great to see you", "Welcome home", "Hi there"];
                } else if (hour >= 12) {
                  greeting = ["Good afternoon", "Afternoon", "Good to see you"];
                } else if (hour >= 5) {
                  greeting = ["Good morning", "Morning", "Rise and shine", "Hello", "Hi there"];
                } else {
                  greeting = ["Hello", "Hi there", "Greetings", "Hey", "Welcome", "Nice to see you", "Welcome home", "What's up", "Hi", "Hello there", "Hope you're well", "Hey there", "What's happening", "Good to see you"];
                }
                const userName = user ? user.name : 'Guest';
                return greeting[Math.floor(Math.random() * greeting.length)] + ', ' + userName;
              ]]]
            label: |
              [[[
                var messages = [];
                if (states['sensor.home_assistant_restart_required'].state == 'true') {
                  messages.push("One or more updates require a restart.");
                }
                if (states['binary_sensor.pending_updates'].state == 'on') {
                  messages.push("There are one or more updates pending install.");
                }
                if (messages.length > 0) {
                  return messages.join(' ');
                } else {
                  return "There are currently no issues.";
                }
              ]]]
            styles:
              card:
                - padding: 18px 18px 36px 13px
                - background-color: var(--contrast1)
              name:
                - font-size: 24px
                - justify-self: start
                - align-self: center
                - text-align: left
                - white-space: normal
                - word-wrap: break-word
                - overflow: hidden
              label:
                - font-size: 18px
                - color: var(--contrast10)
                - justify-self: start
                - align-self: center
                - text-align: left
                - white-space: normal
                - word-wrap: break-word
                - overflow: hidden
                - padding-top: 18px
          - type: custom:button-card
            tap_action:
              action: assist
              pipeline_id: 01j3dtc81ztpv45arhcv9zqakd
            custom_fields:
              assist:
                card:
                  type: picture
                  image: /local/Chatbot/chatbot_700x700.webp
            styles:
              grid:
                - grid-template-areas: |
                    "assist"
                - grid-template-columns: 1fr
                - grid-template-rows: 1fr
              card:
                - width: 75px
                - height: 75px
                - justify-self: center
                - align-self: center
                - margin-top: 50%
                - transform: translateY(-25%)
              custom_fields:
                assist:
                  - width: 100%
                  - height: 100%
                  - justify-self: center
                  - align-self: center
                  - margin-top: '-5px'
                  - z-index: -1
      - event_grouping: true
        drop_todayevents_from: '10:00:00'
        next_days: 7
        pattern:
          - icon: m3s:grass-rounded
            color: brown
            type: organic
            pattern: Garden Waste
          - icon: mdi:recycle-variant
            color: grey
            type: grey
            pattern: Recycling
          - icon: mdi:trash-can-outline
            color: green
            type: waste
            pattern: General Waste
          - icon: mdi:dump-truck
            color: blue
            type: others
        day_style: counter
        day_style_format: yyyy.MM.dd
        card_style: chip
        alignment_style: left
        color_mode: icon
        items_per_row: 3
        refresh_rate: 60
        with_label: false
        type: custom:trash-card
        entities:
          - calendar.bin_collection
        filter_events: false
        use_summary: false
        hide_time_range: true
        full_size: false
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            icon: m3s:chair-rounded
            name: Living Room
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/living-room
          - type: custom:button-card
            icon: m3s:kitchen-rounded
            name: Kitchen
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/kitchen
          - type: custom:button-card
            icon: m3s:hallway-rounded
            name: Hallway
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/hallway
          - type: custom:button-card
            icon: m3s:single-bed-rounded
            name: James' Bedroom
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/james-bedroom
          - type: custom:button-card
            icon: m3s:single-bed-rounded
            name: Rebecca's Bedroom
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/rebecca-s-bedroom
          - type: custom:button-card
            icon: m3s:single-bed-rounded
            name: Daniel's Bedroom
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/daniel-s-bedroom
          - type: custom:button-card
            icon: m3s:king-bed-rounded
            name: Master Bedroom
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/master-bedroom
        columns: 3
        title: Rooms
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            icon: mdi:home-automation
            name: Automations
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /config/automation/dashboard
          - type: custom:button-card
            icon: mdi:calendar
            name: Calendar
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /profile/general
          - type: custom:button-card
            icon: mdi:lightning-bolt
            name: Energy
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /energy
          - type: custom:button-card
            icon: mdi:network-outline
            name: Network
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/network
          - type: custom:button-card
            icon: mdi:home-assistant
            name: System
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/system
          - type: custom:button-card
            icon: mdi:cog-outline
            name: Settings
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
                - padding: 5%
              icon:
                - width: 50%
                - height: 100%
              name:
                - padding: 5%
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: end
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: 1fr 1fr
            tap_action:
              action: navigate
              navigation_path: /profile/general
        columns: 3
        title: Extras
    subview: false
    type: custom:vertical-layout
  - title: Living Room
    path: living-room
    subview: true
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:gap-card
        height: 8
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            icon: m3s:tv-gen-rounded
            name: Living Room TV
            entity: media_player.living_room_tv
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: playing
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: idle
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on' || entity.state == 'playing' || entity.state == 'idle') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/living-room-tv
            hold_action:
              action: more-info
        columns: 3
        title: Managed Devices
    type: custom:vertical-layout
  - title: James' Bedroom
    path: james-bedroom
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:mushroom-chips-card
            chips:
              - type: back
                card_mod:
                  style: |
                    ha-card {
                      background: transparent;
                      --chip-background: transparent;
                      box-shadow: none;
                      margin: 18px 0px 18px 0px;
                    }
          - type: custom:button-card
            name: |
              [[[
                return entity.attributes.friendly_name;
              ]]]
            label: |
              [[[
                return states['sensor.james_samsung_galaxy_s24_geocoded_location'].state.split(',')[0];
              ]]]
            show_name: true
            show_label: true
            show_state: false
            show_icon: true
            show_entity_picture: true
            entity: person.james
            tap_action:
              action: more-info
            styles:
              card:
                - width: 100%
                - background-color: var(--contrast2)
                - padding: 10px 10px 10px 0px
                - margin-top: 8px
                - border-radius: 99vh
              grid:
                - grid-template-areas: |
                    "i n btn"
                    "i l btn"
                - grid-template-columns: 60px 1fr min-content
                - grid-template-rows: min-content min-content
              name:
                - align-self: end
                - justify-self: start
                - background: none
                - padding-left: 0px
                - font-size: 14px
                - font-weight: 600
              label:
                - align-self: start
                - justify-self: start
                - background: none
                - padding: 0px
                - padding-top: 0px
                - color: var(--contrast10)
                - font-size: 12px
              img_cell:
                - justify-content: start
                - width: 40px
                - height: 40px
                - border-radius: 99vh
              icon:
                - color: var(--contrast1)
                - justify-content: start
                - align-content: center
              entity_picture:
                - justify-content: start
                - position: absolute
                - width: 40px
                - height: 40px
                - left: 0ppx
                - bottom: 0px
                - margin: 0px 0px 0px 0px
                - border-radius: 500px
              custom_fields:
                btn:
                  - align-self: center
                  - justify-self: end
            custom_fields:
              btn:
                card:
                  type: custom:mushroom-chips-card
                  chips:
                    - type: entity
                      tap_action:
                        action: more-info
                      entity: sensor.james_samsung_galaxy_s24_battery_level
                      content_info: none
                      card_mod:
                        style: |
                          ha-card {
                            --color: {{ 'var(--contrast20)' if states('sensor.sm_s926b_battery_level') | float > 10  else 'var(--black)' }};
                            --chip-background: {{ 'var(--contrast4)' if states('sensor.sm_s926b_battery_level') | float > 10  else 'var(--red)' }};
                            padding: 0px!important;
                            border-radius: 100px!important;
                            --primary-text-color: var(--contrast20);
                          }
      - type: custom:gap-card
        height: 8
      - type: custom:mushroom-chips-card
        chips:
          - type: template
            entity: climate.james_sensibo_air_pro
            content: >
              {{ state_attr('climate.james_sensibo_air_pro',
              'current_temperature') }}°C
          - type: entity
            entity: sensor.james_monzo_current_account_balance
            tap_action:
              action: more-info
            hold_action:
              action: more-info
            double_tap_action:
              action: none
          - type: entity
            entity: sensor.james_bedroom_speaker_alarms
            tap_action:
              action: more-info
            hold_action:
              action: more-info
            double_tap_action:
              action: none
            use_entity_picture: false
          - type: entity
            entity: sensor.james_bedroom_total_power
            tap_action:
              action: more-info
            hold_action:
              action: more-info
            double_tap_action:
              action: none
            use_entity_picture: false
        alignment: end
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: light.james_bedroom_light
            name: Bedroom Light
            icon: m3s:light-outlined
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: m3s:table-lamp-rounded
            name: Lamp
            entity: switch.james_swing_arm_lamp_smart_plug_switch_2
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: mdi:hvac
            name: Air Conditioner
            entity: climate.pro_breeze_5000_btu_smart_pac
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: cool
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: fan
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'cool' || entity.state == 'fan') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: m3s:tv-gen-rounded
            name: TV
            entity: media_player.james_chromecast
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: playing
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: idle
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on' || entity.state == 'playing' || entity.state == 'idle') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: more-info
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: m3s:robot-rounded
            name: SwitchBot
            entity: switch.james_switchbot
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: mdi:printer-3d
            entity: device_tracker.james_bambu_lab_p1s
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: not_home
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: home
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'home') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/bambu-lab-p1s
            hold_action:
              action: more-info
        columns: 3
        title: Managed Devices
      - type: custom:gap-card
        height: 32
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: binary_sensor.james_pc_status
            name: James' PC
            icon: mdi:desktop-tower-monitor
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: none
            hold_action:
              action: more-info
        columns: 3
        title: Un-managed Devices
      - type: custom:gap-card
        height: 32
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            name: Turn ON TV and Xbox
            icon: phu:xbox
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
                - color: var(--contrast20)
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                i2:
                  - justify-self: start
                  - align-self: start
                  - margin-left: 25%
              grid:
                - grid-template-areas: |
                    "i i2 ."
                    "n n n"
                - grid-template-rows: min-content 1fr
                - grid-template-columns: min-content 1fr 1fr
            custom_fields:
              i2: |
                [[[
                    return `
                      <ha-icon
                      icon="phu:lg-oled55"
                      style="
                        background-color: var(--contrast4);
                        padding-top: 3.5px;
                        padding-left: 7.5px;
                        padding-right: 7.5px;
                        padding-bottom: 11.5px;
                        width: 15px;
                        height: 15px;
                        border-radius: 99vh;
                        color: var(--contrast20);
                      ">
                      </ha-icon>`;
                ]]]
            tap_action:
              action: call-service
              service: automation.trigger
              service_data:
                entity_id: automation.turn_on_tv_and_xbox_2
            hold_action:
              action: more-info
        columns: 3
        title: Automations
      - type: custom:gap-card
        height: 32
    type: custom:vertical-layout
    subview: true
  - title: Daniel's Bedroom
    path: daniel-s-bedroom
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:mushroom-chips-card
            chips:
              - type: back
                card_mod:
                  style: |
                    ha-card {
                      background: transparent;
                      --chip-background: transparent;
                      box-shadow: none;
                      margin: 18px 0px 18px 0px;
                    }
          - type: custom:button-card
            name: |
              [[[
                return entity.attributes.friendly_name;
              ]]]
            label: |
              [[[
                return states['device_tracker.dans_pixel_6'].state == 'home' ? "Home" : "Away";
              ]]]
            show_name: true
            show_label: true
            show_state: false
            show_icon: true
            show_entity_picture: true
            entity: person.daniel
            tap_action:
              action: more-info
            styles:
              card:
                - width: 100%
                - background-color: var(--contrast2)
                - padding: 10px 10px 10px 0px
                - margin-top: 8px
                - border-radius: 99vh
              grid:
                - grid-template-areas: |
                    "i n"
                    "i l"
                - grid-template-columns: 60px 1fr
                - grid-template-rows: min-content
              name:
                - align-self: end
                - justify-self: start
                - background: none
                - padding-left: 0px
                - font-size: 14px
                - font-weight: 600
                - padding-right: 12px
              label:
                - align-self: start
                - justify-self: start
                - background: none
                - padding: 0px
                - padding-top: 0px
                - color: var(--contrast10)
                - font-size: 12px
              img_cell:
                - justify-content: start
                - width: 40px
                - height: 40px
                - border-radius: 99vh
              icon:
                - color: var(--contrast1)
                - justify-content: start
                - align-content: center
              entity_picture:
                - justify-content: start
                - position: absolute
                - width: 40px
                - height: 40px
                - left: 0ppx
                - bottom: 0px
                - margin: 0px 0px 0px 0px
                - border-radius: 500px
      - type: custom:gap-card
        height: 8
      - type: custom:mushroom-chips-card
        chips:
          - type: entity
            entity: sensor.daniel_s_bedroom_total_power
            tap_action:
              action: more-info
            hold_action:
              action: more-info
            double_tap_action:
              action: none
            use_entity_picture: false
        alignment: end
      - type: custom:gap-card
        height: 8
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: light.daniel_s_bedroom_light
            name: Bedroom Light
            icon: m3s:light-outlined
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
        columns: 3
        title: Managed Devices
      - type: custom:gap-card
        height: 32
      - type: conditional
        conditions:
          - condition: state
            entity: light.daniel_s_bedroom_light
            state: 'on'
        card:
          square: true
          type: grid
          cards:
            - type: custom:button-card
              entity: scene.dan_s_bedroom_concentrate
              name: Concentrate Mode
              icon: mdi:brain
              show_name: true
              show_icon: true
              aspect_ratio: 1/1
              styles:
                card:
                  - box-shadow: none
                  - padding: 10%
                img_cell:
                  - border-radius: 100%
                  - width: 30px
                  - height: 30px
                  - background-color: var(--contrast4)
                  - justify-self: start
                  - align-self: start
                icon:
                  - width: 50%
                  - height: 100%
                name:
                  - margin-top: 10%
                  - color: var(--contrast20)
                  - font-size: 0.75em
                  - text-align: left
                  - white-space: normal
                  - word-break: break-word
                  - justify-self: start
                  - align-self: center
                custom_fields:
                  second:
                    - text-align: left
                    - align-self: end
                    - justify-self: end
                    - margin-bottom: '-8px'
                grid:
                  - grid-template-areas: |
                      "i ."
                      "n n"
                      ". second"
                  - grid-template-rows: min-content 1fr min-content
                  - grid-template-columns: 1fr 1fr
              state:
                - value: 'off'
                  styles:
                    card:
                      - background-color: var(--ha-card-background)
                    icon:
                      - color: var(--contrast20)
                    img_cell:
                      - background-color: var(--contrast4)
                - value: 'on'
                  styles:
                    card:
                      - background-color: var(--contrast20)
                    name:
                      - color: var(--contrast1)
                    icon:
                      - color: var(--contrast1)
                    img_cell:
                      - background-color: var(--contrast16)
                - value: unavailable
                  styles:
                    icon:
                      - color: red
                    img_cell:
                      - background-color: rgba(255,0,0,var(--color-tint))
              custom_fields:
                second: |
                  [[[
                    if (entity.state == 'on') {
                      return `<ha-icon
                        icon="mdi:toggle-switch"
                        style="width: 40px; height: min-content; color: var(--contrast1);">
                        </ha-icon>`;
                    } else {
                      return `<ha-icon
                        icon="mdi:toggle-switch-off"
                        style="width: 40px; height: min-content; color: var(--contrast4);">
                        </ha-icon>`;
                    }
                  ]]]
              tap_action:
                action: toggle
              hold_action:
                action: more-info
            - type: custom:button-card
              entity: scene.dan_s_bedroom_dimmed
              name: Dimmed Mode
              icon: m3s:keyboard-arrow-down-rounded
              show_name: true
              show_icon: true
              aspect_ratio: 1/1
              styles:
                card:
                  - box-shadow: none
                  - padding: 10%
                img_cell:
                  - border-radius: 100%
                  - width: 30px
                  - height: 30px
                  - background-color: var(--contrast4)
                  - justify-self: start
                  - align-self: start
                icon:
                  - width: 50%
                  - height: 100%
                name:
                  - margin-top: 10%
                  - color: var(--contrast20)
                  - font-size: 0.75em
                  - text-align: left
                  - white-space: normal
                  - word-break: break-word
                  - justify-self: start
                  - align-self: center
                custom_fields:
                  second:
                    - text-align: left
                    - align-self: end
                    - justify-self: end
                    - margin-bottom: '-8px'
                grid:
                  - grid-template-areas: |
                      "i ."
                      "n n"
                      ". second"
                  - grid-template-rows: min-content 1fr min-content
                  - grid-template-columns: 1fr 1fr
              state:
                - value: 'off'
                  styles:
                    card:
                      - background-color: var(--ha-card-background)
                    icon:
                      - color: var(--contrast20)
                    img_cell:
                      - background-color: var(--contrast4)
                - value: 'on'
                  styles:
                    card:
                      - background-color: var(--contrast20)
                    name:
                      - color: var(--contrast1)
                    icon:
                      - color: var(--contrast1)
                    img_cell:
                      - background-color: var(--contrast16)
                - value: unavailable
                  styles:
                    icon:
                      - color: red
                    img_cell:
                      - background-color: rgba(255,0,0,var(--color-tint))
              custom_fields:
                second: |
                  [[[
                    if (entity.state == 'on') {
                      return `<ha-icon
                        icon="mdi:toggle-switch"
                        style="width: 40px; height: min-content; color: var(--contrast1);">
                        </ha-icon>`;
                    } else {
                      return `<ha-icon
                        icon="mdi:toggle-switch-off"
                        style="width: 40px; height: min-content; color: var(--contrast4);">
                        </ha-icon>`;
                    }
                  ]]]
              tap_action:
                action: toggle
              hold_action:
                action: more-info
            - type: custom:button-card
              entity: scene.dan_s_bedroom_nebula
              name: Nebula Mode
              icon: m3s:star-rounded-filled
              show_name: true
              show_icon: true
              aspect_ratio: 1/1
              styles:
                card:
                  - box-shadow: none
                  - padding: 10%
                img_cell:
                  - border-radius: 100%
                  - width: 30px
                  - height: 30px
                  - background-color: var(--contrast4)
                  - justify-self: start
                  - align-self: start
                icon:
                  - width: 50%
                  - height: 100%
                name:
                  - margin-top: 10%
                  - color: var(--contrast20)
                  - font-size: 0.75em
                  - text-align: left
                  - white-space: normal
                  - word-break: break-word
                  - justify-self: start
                  - align-self: center
                custom_fields:
                  second:
                    - text-align: left
                    - align-self: end
                    - justify-self: end
                    - margin-bottom: '-8px'
                grid:
                  - grid-template-areas: |
                      "i ."
                      "n n"
                      ". second"
                  - grid-template-rows: min-content 1fr min-content
                  - grid-template-columns: 1fr 1fr
              state:
                - value: 'off'
                  styles:
                    card:
                      - background-color: var(--ha-card-background)
                    icon:
                      - color: var(--contrast20)
                    img_cell:
                      - background-color: var(--contrast4)
                - value: 'on'
                  styles:
                    card:
                      - background-color: var(--contrast20)
                    name:
                      - color: var(--contrast1)
                    icon:
                      - color: var(--contrast1)
                    img_cell:
                      - background-color: var(--contrast16)
                - value: unavailable
                  styles:
                    icon:
                      - color: red
                    img_cell:
                      - background-color: rgba(255,0,0,var(--color-tint))
              custom_fields:
                second: |
                  [[[
                    if (entity.state == 'on') {
                      return `<ha-icon
                        icon="mdi:toggle-switch"
                        style="width: 40px; height: min-content; color: var(--contrast1);">
                        </ha-icon>`;
                    } else {
                      return `<ha-icon
                        icon="mdi:toggle-switch-off"
                        style="width: 40px; height: min-content; color: var(--contrast4);">
                        </ha-icon>`;
                    }
                  ]]]
              tap_action:
                action: toggle
              hold_action:
                action: more-info
          columns: 3
          title: Light Actions
      - type: custom:gap-card
        height: 32
    subview: true
    type: custom:vertical-layout
  - title: Rebecca's Bedroom
    path: rebecca-s-bedroom
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:mushroom-chips-card
            chips:
              - type: back
                card_mod:
                  style: |
                    ha-card {
                      background: transparent;
                      --chip-background: transparent;
                      box-shadow: none;
                      margin: 18px 0px 18px 0px;
                    }
          - type: custom:button-card
            name: |
              [[[
                return entity.attributes.friendly_name;
              ]]]
            label: |
              [[[
                return entity.state == 'home' ? "Home" : "Away";
              ]]]
            show_name: true
            show_label: true
            show_state: false
            show_icon: true
            show_entity_picture: true
            entity: person.rebecca
            tap_action:
              action: more-info
            styles:
              card:
                - width: 100%
                - background-color: var(--contrast2)
                - padding: 10px 10px 10px 0px
                - margin-top: 8px
                - border-radius: 99vh
              grid:
                - grid-template-areas: |
                    "i n"
                    "i l"
                - grid-template-columns: 60px 1fr
                - grid-template-rows: min-content
              name:
                - align-self: end
                - justify-self: start
                - background: none
                - padding-left: 0px
                - font-size: 14px
                - font-weight: 600
                - padding-right: 12px
              label:
                - align-self: start
                - justify-self: start
                - background: none
                - padding: 0px
                - padding-top: 0px
                - color: var(--contrast10)
                - font-size: 12px
              img_cell:
                - justify-content: start
                - width: 40px
                - height: 40px
                - border-radius: 99vh
              icon:
                - color: var(--contrast1)
                - justify-content: start
                - align-content: center
              entity_picture:
                - justify-content: start
                - position: absolute
                - width: 40px
                - height: 40px
                - left: 0ppx
                - bottom: 0px
                - margin: 0px 0px 0px 0px
                - border-radius: 500px
      - type: custom:gap-card
        height: 8
      - type: custom:mushroom-chips-card
        chips:
          - type: entity
            entity: sensor.rebecca_s_bedroom_total_power
            content_info: state
            tap_action:
              action: none
            hold_action:
              action: none
            double_tap_action:
              action: none
            use_entity_picture: false
        alignment: end
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: light.rebecca_s_bedroom_light
            name: Bedroom Light
            icon: m3s:light-outlined
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: toggle
            hold_action:
              action: more-info
          - type: custom:button-card
            icon: m3s:tv-gen-rounded
            name: TV
            entity: media_player.rebecca_s_bedroom_tv
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              custom_fields:
                second:
                  - text-align: left
                  - align-self: end
                  - justify-self: end
                  - margin-bottom: '-8px'
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". second"
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: 'off'
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: 'on'
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: playing
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: idle
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            custom_fields:
              second: |
                [[[
                  if (entity.state == 'on' || entity.state == 'playing' || entity.state == 'idle') {
                    return `<ha-icon
                      icon="mdi:toggle-switch"
                      style="width: 40px; height: min-content; color: var(--contrast1);">
                      </ha-icon>`;
                  } else {
                    return `<ha-icon
                      icon="mdi:toggle-switch-off"
                      style="width: 40px; height: min-content; color: var(--contrast4);">
                      </ha-icon>`;
                  }
                ]]]
            tap_action:
              action: more-info
            hold_action:
              action: more-info
        columns: 3
        title: Managed Devices
      - type: custom:gap-card
        height: 32
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: device_tracker.rebecca_s_air_conditioner_2
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: not_home
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: home
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: nonw
            hold_action:
              action: none
        columns: 3
        title: Un-managed Devices
      - type: custom:gap-card
        height: 32
    subview: true
    type: custom:vertical-layout
  - title: Kitchen
    path: kitchen
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: vertical-stack
        cards:
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/images/devices/Canon_MG3600.png
                show_label: false
                show_name: false
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - width: 150px
                    - height: 100%
                    - padding-top: 18px
                    - padding-bottom: 18px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i" 
                        "i"
                    - grid-template-columns: 1fr
                    - grid-template-rows: 1fr 1fr
                  img_cell:
                    - justify-content: center
                    - width: 100px
                  entity_picture:
                    - width: 100%
              - type: entities
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
                      #states {
                        padding-top: 0px !important;
                        padding-left: 0px !important;
                        padding-right: 0px !important;
                        padding-bottom: 0px !important;
                      }
                      #states > div {
                        margin-top: 8px !important;
                        margin-bottom: 8px !important;
                        margin-left: 0px !important;
                        margin-right: 0px !important;
                      }
                entities:
                  - type: divider
                  - type: custom:button-card
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Model
                      val: |
                        [[[
                          return "Canon MG3600" ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.canon_mg3600_black
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Black Ink
                      val: |
                        [[[
                          return entity.state;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.canon_mg3600_color
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Colour Ink
                      val: |
                        [[[
                          return entity.state;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 1fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
        title: Kitchen Printer
      - type: custom:gap-card
        height: 36
      - type: vertical-stack
        title: Fridge Freezer
        cards:
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/images/devices/Beko_CF6004AP.png
                show_label: false
                show_name: false
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - width: 100px
                    - height: 100%
                    - padding-top: 18px
                    - padding-bottom: 18px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i" 
                        "i"
                    - grid-template-columns: 1fr
                    - grid-template-rows: 1fr 1fr
                  img_cell:
                    - justify-content: center
                    - width: 100%
                    - height: 100%
                  entity_picture:
                    - height: 100%
                    - width: auto
                  icon:
                    - width: 70%
              - type: entities
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
                      #states {
                        padding-top: 0px !important;
                        padding-left: 0px !important;
                        padding-right: 0px !important;
                        padding-bottom: 0px !important;
                      }
                      #states > div {
                        margin-top: 8px !important;
                        margin-bottom: 8px !important;
                        margin-left: 0px !important;
                        margin-right: 0px !important;
                      }
                entities:
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.beko_fridge_freezer_model
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Model
                      val: |
                        [[[
                          return entity.state ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.kitchen_beko_fridge_freezer_power
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Power
                      val: |
                        [[[
                          return entity.state + ' W' ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.kitchen_beko_fridge_freezer_energy_daily
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Energy Consumed
                      val: |
                        [[[
                          return entity.state + ' KWh' ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 1fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
      - type: custom:gap-card
        height: 36
      - type: vertical-stack
        title: Freezer
        cards:
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                entity_picture: /local/images/devices/Beko_FFG1545W.png
                show_label: false
                show_name: false
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - width: 100px
                    - height: 100%
                    - padding-top: 18px
                    - padding-bottom: 18px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i" 
                        "i"
                    - grid-template-columns: 1fr
                    - grid-template-rows: 1fr 1fr
                  img_cell:
                    - justify-content: center
                    - width: 100%
                    - height: 100%
                  entity_picture:
                    - height: 100%
                    - width: auto
                  icon:
                    - width: 70%
              - type: entities
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
                      #states {
                        padding-top: 0px !important;
                        padding-left: 0px !important;
                        padding-right: 0px !important;
                        padding-bottom: 0px !important;
                      }
                      #states > div {
                        margin-top: 8px !important;
                        margin-bottom: 8px !important;
                        margin-left: 0px !important;
                        margin-right: 0px !important;
                      }
                entities:
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.beko_freezer_model
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Model
                      val: |
                        [[[
                          return entity.state ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.kitchen_beko_freezer_power_2
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Power
                      val: |
                        [[[
                          return entity.state + ' W' ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 3fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
                  - type: custom:button-card
                    entity: sensor.kitchen_beko_freezer_energy_2_daily
                    show_name: false
                    show_label: false
                    show_state: false
                    show_icon: false
                    custom_fields:
                      title: Energy Consumed
                      val: |
                        [[[
                          return entity.state + ' KWh' ;
                        ]]]
                    styles:
                      card:
                        - padding: 18px
                        - background-color: transparent
                      grid:
                        - grid-template-areas: |
                            "title val"
                        - grid-template-columns: 1fr 1fr
                      custom_fields:
                        title:
                          - justify-self: start
                          - font-weight: 500
                        val:
                          - justify-self: end
                          - color: var(--contrast10)
                  - type: divider
    subview: true
    type: custom:vertical-layout
  - title: Master Bedroom
    path: master-bedroom
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:mushroom-chips-card
            chips:
              - type: back
                card_mod:
                  style: |
                    ha-card {
                      background: transparent;
                      --chip-background: transparent;
                      box-shadow: none;
                      margin: 18px 0px 18px 0px;
                    }
          - type: custom:button-card
            name: |
              [[[
                return entity.attributes.friendly_name;
              ]]]
            label: |
              [[[
                return entity.state == 'home' ? "Home" : "Away";
              ]]]
            show_name: true
            show_label: true
            show_state: false
            show_icon: true
            show_entity_picture: true
            entity: person.darron
            tap_action:
              action: more-info
            styles:
              card:
                - width: 100%
                - background-color: var(--contrast2)
                - padding: 10px 10px 10px 0px
                - margin-top: 8px
                - border-radius: 99vh
              grid:
                - grid-template-areas: |
                    "i n"
                    "i l"
                - grid-template-columns: 60px 1fr
                - grid-template-rows: min-content
              name:
                - align-self: end
                - justify-self: start
                - background: none
                - padding-left: 0px
                - font-size: 14px
                - font-weight: 600
                - padding-right: 12px
              label:
                - align-self: start
                - justify-self: start
                - background: none
                - padding: 0px
                - padding-top: 0px
                - color: var(--contrast10)
                - font-size: 12px
              img_cell:
                - justify-content: start
                - width: 40px
                - height: 40px
                - border-radius: 99vh
              icon:
                - color: var(--contrast1)
                - justify-content: start
                - align-content: center
              entity_picture:
                - justify-content: start
                - position: absolute
                - width: 40px
                - height: 40px
                - left: 0ppx
                - bottom: 0px
                - margin: 0px 0px 0px 0px
                - border-radius: 500px
          - type: custom:button-card
            name: |
              [[[
                return entity.attributes.friendly_name;
              ]]]
            label: |
              [[[
                return entity.state == 'home' ? "Home" : "Away";
              ]]]
            show_name: true
            show_label: true
            show_state: false
            show_icon: true
            show_entity_picture: true
            entity: person.dawn
            tap_action:
              action: more-info
            styles:
              card:
                - width: 100%
                - background-color: var(--contrast2)
                - padding: 10px 10px 10px 0px
                - margin-top: 8px
                - border-radius: 99vh
              grid:
                - grid-template-areas: |
                    "i n"
                    "i l"
                - grid-template-columns: 60px 1fr
                - grid-template-rows: min-content
              name:
                - align-self: end
                - justify-self: start
                - background: none
                - padding-left: 0px
                - font-size: 14px
                - font-weight: 600
                - padding-right: 12px
              label:
                - align-self: start
                - justify-self: start
                - background: none
                - padding: 0px
                - padding-top: 0px
                - color: var(--contrast10)
                - font-size: 12px
              img_cell:
                - justify-content: start
                - width: 40px
                - height: 40px
                - border-radius: 99vh
              icon:
                - color: var(--contrast1)
                - justify-content: start
                - align-content: center
              entity_picture:
                - justify-content: start
                - position: absolute
                - width: 40px
                - height: 40px
                - left: 0ppx
                - bottom: 0px
                - margin: 0px 0px 0px 0px
                - border-radius: 500px
      - type: custom:gap-card
        height: 8
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: device_tracker.unifi_default_90_98_77_65_dc_6e
            name: Master Bedroom TV
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: home
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: not_home
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: none
            hold_action:
              action: none
        columns: 3
        title: Un-managed Devices
    subview: true
  - title: System
    path: system
    type: custom:vertical-layout
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 8px !important;
                    margin-bottom: 8px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity: device_tracker.homeassistant_2
                entity_picture: /local/images/devices/pi-4.png
                name: Home Assistant
                label: raspberrypi4-64
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 18px
                    - height: 130px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: center
                    - padding-right: 18px
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 50%
                    - justify-self: center
                    - align-self: center
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: Raspberry Pi 4
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.james
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      function formatUptime(lastBoot) {
                        const now = new Date();
                        const lastBootDate = new Date(lastBoot);
                        const diffMs = now - lastBootDate;
                        const diffDays = Math.floor(diffMs / (1000 * 60 * 60 * 24));
                        const diffHours = Math.floor((diffMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                        const diffMinutes = Math.floor((diffMs % (1000 * 60 * 60)) / (1000 * 60));
                        return `${diffDays}d ${diffHours}h ${diffMinutes}m`;
                      }
                      const lastBoot = states['sensor.last_boot'].state;
                      return formatUptime(lastBoot);
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: CPU Architecture
                  val: aarch64
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Operating System Version
                  val: |
                    [[[ 
                      return states['update.home_assistant_operating_system_update'].attributes.installed_version ;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Core Version
                  val: |
                    [[[ 
                      return states['update.home_assistant_core_update'].attributes.installed_version ;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Supervisor Version
                  val: |
                    [[[ 
                      return states['update.home_assistant_supervisor_update'].attributes.installed_version ;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: IPV4 Address
                  val: |
                    [[[ 
                      return states['sensor.system_monitor_ipv4_address_end0'].state ;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Last Boot
                  val: |
                    [[[
                      const lastBoot = new Date(states['sensor.last_boot'].state);
                      const now = new Date();
                      const diffMs = now - lastBoot;
                      const diffDays = Math.floor(diffMs / (1000 * 60 * 60 * 24));
                      const diffHours = Math.floor((diffMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                      const diffMinutes = Math.floor((diffMs % (1000 * 60 * 60)) / (1000 * 60));
                      const formattedTime = `${diffDays}d ${diffHours}h ${diffMinutes}m`;
                      return `<span style="color: var(--text-color-sensor);">${formattedTime}</span>`;
                    ]]]  
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
      - type: custom:uptime-card
        entity: binary_sensor.home_assistant_online
        title_adaptive_color: false
        status_adaptive_color: false
        icon_adaptive_color: false
        tooltip_adaptive_color: false
        show:
          header: false
          title: false
          icon: false
          status: false
          timeline: true
          footer: true
          average: false
        tooltip:
          hour24: true
        alignment:
          tooltip_first: false
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
              }
      - type: custom:gap-card
        height: 36
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 8px !important;
                    margin-bottom: 8px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                name: Performance
                show_name: true
                styles:
                  card:
                    - padding-left: 18px
                    - height: 56px
                    - background-color: transparent
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
              - type: custom:mini-graph-card
                entities:
                  - entity: sensor.processor_use
                    name: CPU
                    color: '#00bb33'
                    show_state: true
                    show_indicator: false
                    show_legend: true
                    show_points: false
                    show_fill: true
                    show_line: true
                    show_graph: true
                  - entity: sensor.disk_use_percent
                    name: Storage
                    color: '#bb0018'
                    show_state: true
                    show_indicator: false
                    show_legend: true
                    show_points: false
                    show_fill: true
                    show_line: true
                    show_graph: true
                  - entity: sensor.memory_use_percent
                    name: RAM
                    color: '#2196f3'
                    show_state: true
                    show_indicator: false
                    show_legend: true
                    show_points: false
                    show_fill: true
                    show_line: true
                    show_graph: true
                hours_to_show: 12
                line_width: 3
                font_size: 100
                animate: true
                show:
                  name: false
                  state: false
                  icon: false
                  labels: false
                  labels_secondary: true
                  legend: true
                  fill: fade
                  points: false
                card_mod:
                  style: |
                    .graph {
                      background: transparent !important;
                      padding-bottom: 18px;
                    }
                    ha-card {
                      background: transparent !important;
                      box-shadow: none !important;
                      border-radius: 0px;
                      padding-bottom: 18px;
                    }
              - type: custom:gap-card
                height: 36
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: CPU
                  val: |
                    [[[
                      return states['sensor.processor_use'].state + '%';
                    ]]]
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Temperature
                  val: |
                    [[[
                      return states['sensor.processor_temperature'].state + '°C';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Memory
                  val: |
                    [[[
                      return states['sensor.memory_use_percent'].state + '%';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Storage
                  val: |
                    [[[ 
                      return states['sensor.disk_use_percent'].state + '%';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
      - type: custom:gap-card
        height: 36
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
              }
        cards:
          - type: custom:button-card
            name: Entity Statistics
            show_name: true
            styles:
              card:
                - padding: 18px
                - height: min-content
                - background-color: transparent
              name:
                - font-weight: 500
                - justify-self: start
                - align-self: end
                - font-size: 1.5rem
          - type: custom:auto-entities
            sort:
              method: state
              numeric: true
              reverse: true
            card:
              type: entities
              card_mod:
                style:
                  .: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
                    #states {
                      padding-top: 0px !important;
                      padding-left: 0px !important;
                      padding-right: 0px !important;
                      padding-bottom: 0px !important;
                    }
                    #states > div {
                      margin-top: 8px !important;
                      margin-bottom: 0px !important;
                      margin-left: 0px !important;
                      margin-right: 0px !important;
                    }
            filter:
              include:
                - entity_id: '*number_of*'
                  options:
                    type: custom:button-card
                    entity: this.entity_id
                    show_name: true
                    show_label: false
                    show_icon: false
                    show_state: true
                    tap_action:
                      action: more-info
                    name: >
                      [[[ return entity.attributes.friendly_name.replace("Number
                      of ", ""); ]]]
                    styles:
                      card:
                        - padding: 0px
                        - border-radius: 0px
                        - margin: 0px
                      grid:
                        - grid-template-areas: |
                            "d d"
                            "n s"
                        - grid-template-columns: 1fr 1fr
                        - grid-template-rows: min-content 64px
                      name:
                        - padding-top: 8px
                        - padding-left: 18px
                        - justify-self: start
                        - font-weight: 500
                        - align-self: center
                      state:
                        - padding-top: 8px
                        - padding-right: 18px
                        - justify-self: end
                        - color: var(--contrast10)
                        - align-self: center
                      custom_fields:
                        divider:
                          - padding: 0px
                          - margin: 0px
                    custom_fields:
                      d:
                        card:
                          type: entities
                          entities:
                            - type: divider
                          card_mod:
                            style: |
                              #states {
                                padding: 0px !important;
                                margin: 0px !important;
                              }
                              ha-card {
                                background-color: transparent;
                                box-shadow: none;
                                padding: 0px;
                              }
                    card_mod:
                      style: |
                        ha-card {
                          background-color: transparent;
                          box-shadow: none;
                          padding: 0px;
                        }
    subview: true
  - title: Hallway
    path: hallway
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: device_tracker.cloud_gateway_ultra_3
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: not_home
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: home
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/cloud-gateway-ultra
            hold_action:
              action: none
        columns: 3
        title: Managed Devices
      - type: custom:gap-card
        height: 32
      - square: true
        type: grid
        cards:
          - type: custom:button-card
            entity: sensor.bt_smart_hub_2_system_uptime_in_seconds
            name: BT Smart Hub 2
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - operator: '=='
                value: 0
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - operator: '>='
                value: 1
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/bt-smart-hub-2
            hold_action:
              action: none
          - type: custom:button-card
            entity: device_tracker.phoenix
            show_name: true
            show_icon: true
            aspect_ratio: 1/1
            styles:
              card:
                - box-shadow: none
                - padding: 10%
              img_cell:
                - border-radius: 100%
                - width: 30px
                - height: 30px
                - background-color: var(--contrast4)
                - justify-self: start
                - align-self: start
              icon:
                - width: 50%
                - height: 100%
              name:
                - margin-top: 10%
                - color: var(--contrast20)
                - font-size: 0.75em
                - text-align: left
                - white-space: normal
                - word-break: break-word
                - justify-self: start
                - align-self: center
              grid:
                - grid-template-areas: |
                    "i ."
                    "n n"
                    ". ."
                - grid-template-rows: min-content 1fr min-content
                - grid-template-columns: 1fr 1fr
            state:
              - value: not_home
                styles:
                  card:
                    - background-color: var(--ha-card-background)
                  icon:
                    - color: var(--contrast20)
                  img_cell:
                    - background-color: var(--contrast4)
              - value: home
                styles:
                  card:
                    - background-color: var(--contrast20)
                  name:
                    - color: var(--contrast1)
                  icon:
                    - color: var(--contrast1)
                  img_cell:
                    - background-color: var(--contrast16)
              - value: unavailable
                styles:
                  icon:
                    - color: red
                  img_cell:
                    - background-color: rgba(255,0,0,var(--color-tint))
            tap_action:
              action: navigate
              navigation_path: /dashboard-home/house-mobile-phone
            hold_action:
              action: none
        columns: 3
        title: Un-managed Devices
    subview: true
    type: custom:vertical-layout
  - title: Landing
    path: landing
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:auto-entities
        card:
          type: entities
        filter:
          include:
            - area: Landing
        sort:
          method: friendly_name
    subview: true
  - title: Network
    path: network
    subview: true
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: var(--contrast1);
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: custom:button-card
            name: Wifi Details
            show_name: true
            styles:
              card:
                - padding-top: 0px
                - padding-left: 18px
                - padding-right: 18px
                - padding-bottom: 18px
                - height: min-content
                - background-color: var(--contrast1)
              name:
                - font-weight: 500
                - justify-self: start
                - align-self: end
                - padding-bottom: 3px
                - font-size: 1.5rem
          - square: true
            type: grid
            cards:
              - type: custom:button-card
                aspect_ratio: 1/1
                show_name: false
                show_label: false
                show_state: false
                show_icon: false
                styles:
                  card:
                    - border-radius: 0px
                    - background-color: var(--contrast1)
                  grid:
                    - grid-template-areas: |
                        "stack"
                custom_fields:
                  stack:
                    card:
                      type: custom:stack-in-card
                      card_mod:
                        style:
                          .: |
                            ha-card {
                              background-color: var(--contrast1);
                              box-shadow: none;
                              padding: 0px !important;
                              margin: 0px !important;
                              border-radius: 0px;
                            }
                      cards:
                        - type: entities
                          card_mod:
                            style: |
                              #states {
                                padding-top: 0px !important;
                                padding-left: 0px !important;
                                padding-right: 0px !important;
                                padding-bottom: 0px !important;
                              }
                          entities:
                            - type: custom:button-card
                              name: SSID
                              label: [ssid]
                              show_name: true
                              show_label: true
                              show_state: false
                              show_icon: false
                              styles:
                                name:
                                  - justify-self: start
                                  - padding-left: 18px
                                  - color: var(--contrast10)
                                  - font-size: 12px
                                  - padding-bottom: 3px
                                label:
                                  - justify-self: start
                                  - padding-left: 18px
                                grid:
                                  - grid-template-areas: |
                                      "n"
                                      "l"
                                  - grid-template-columns: 1fr
                                  - grid-template-rows: min-content min-content
                                card:
                                  - background-color: var(--contrast1)
                            - type: custom:button-card
                              name: Password
                              label: [password]
                              show_name: true
                              show_label: true
                              show_state: false
                              show_icon: false
                              styles:
                                name:
                                  - justify-self: start
                                  - padding-left: 18px
                                  - color: var(--contrast10)
                                  - font-size: 12px
                                  - padding-bottom: 3px
                                label:
                                  - justify-self: start
                                  - padding-left: 18px
                                grid:
                                  - grid-template-areas: |
                                      "n"
                                      "l"
                                  - grid-template-columns: 1fr
                                  - grid-template-rows: min-content min-content
                                card:
                                  - background-color: var(--contrast1)
                            - type: custom:button-card
                              name: Scan the QR Code to connect to the home Wifi
                              show_name: true
                              show_label: false
                              show_state: false
                              show_icon: false
                              styles:
                                name:
                                  - justify-self: start
                                  - padding-left: 18px
                                  - padding-right: 18px
                                  - color: var(--contrast10)
                                  - font-size: 12px
                                  - justify-self: start
                                  - align-self: center
                                  - text-align: left
                                  - white-space: normal
                                  - word-wrap: break-word
                                grid:
                                  - grid-template-areas: |
                                      "n"
                                  - grid-template-columns: 1fr
                                  - grid-template-rows: min-content min-content
                                card:
                                  - background-color: var(--contrast1)
              - type: custom:button-card
                aspect_ratio: 1/1
                show_icon: false
                show_name: false
                show_label: false
                show_state: false
                custom_fields:
                  qr:
                    card:
                      type: picture
                      image_entity: image.home_wifi
                      tap_action:
                        action: none
                      hold_action:
                        action: none
                styles:
                  grid:
                    - grid-template-areas: |
                        "qr"
                    - grid-template-columns: 1fr
                    - grid-template-row: qfr
                  card:
                    - padding: 10px
                    - margin: 0
                    - background-color: var(--contrast1)
                  custom_fields:
                    qr:
                      - padding: 10px
                      - height: auto
                      - width: 80%
                      - justify-self: center
                      - align-self: center
                      - text-align: middle
                      - background-color: white
                      - border-radius: 14px
            columns: 2
      - type: custom:gap-card
        height: 32
      - square: false
        type: grid
        cards:
          - type: custom:uptime-card
            card_mod:
              style:
                .: |
                  ha-card {
                    ha-card-background: transparent !important;
                    background-color: transparent !important;
                  }
            entity: binary_sensor.house_internet_connection
            title_adaptive_color: true
            status_adaptive_color: true
            icon_adaptive_color: true
            tooltip_adaptive_color: true
            show:
              title: false
              icon: false
              status: false
              timeline: true
              footer: true
              average: true
              header: true
            tooltip:
              hour24: true
            alignment:
              icon_first: false
            duration:
              quantity: 1
              unit: week
        title: House Internet
        columns: 1
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: var(--contrast1);
                box-shadow: none;
                padding-left: 18px;
                padding-right: 18px;
                margin: 0px !important;
                border-radius: 0px;
              }
        cards:
          - type: custom:mini-graph-card
            entities:
              - entity: sensor.speedtest_download
                name: Download
                color: '#00bb33'
                show_state: true
                show_indicator: false
                show_legend: true
                show_points: true
                show_fill: true
                show_line: true
                show_graph: true
              - entity: sensor.speedtest_upload
                name: Upload
                color: '#bb0018'
                show_state: true
                show_indicator: false
                show_legend: true
                show_points: true
                show_fill: true
                show_line: true
                show_graph: true
            hours_to_show: 24
            line_width: 3
            font_size: 60
            animate: true
            show:
              name: false
              state: true
              icon: false
              labels: false
              labels_secondary: true
              legend: true
              fill: fade
              points: true
            card_mod:
              style: |
                .graph {
                  background: transparent !important;
                  padding-bottom: 18px;
                }
                ha-card {
                  background: transparent !important;
                  box-shadow: none !important;
                  border-radius: 0px;
                  padding-bottom: 18px;
                }
      - type: custom:gap-card
        height: 32
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: entities
            card_mod:
              style: |
                ha-card {
                  background-color: transparent;
                  box-shadow: none;
                  padding: 0px;
                }
                #states {
                  padding-top: 18px !important;
                  padding-left: 0px !important;
                  padding-right: 0px !important;
                  padding-bottom: 18px !important;
                }
            entities:
              - type: custom:button-card
                name: Network Devices
                show_name: true
                styles:
                  card:
                    - padding-top: 0px
                    - padding-left: 18px
                    - padding-bottom: 18px
                    - height: min-content
                    - background-color: transparent
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
              - type: divider
              - type: custom:button-card
                entity: device_tracker.cloud_gateway_ultra
                entity_picture: /local/images/devices/UCG_Ultra.png
                label: UCG Ultra
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 8px
                    - height: 56px
                    - padding-top: 0px
                    - padding-bottom: 0px
                  grid:
                    - grid-template-areas: |
                        "i n connection status_dot arrow" 
                        "i l clients status_dot arrow"
                    - grid-template-columns: 2fr 8fr 2fr 1fr 1fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 600
                    - font-size: 14px
                    - justify-self: start
                    - align-self: end
                    - margin-bottom: 2px
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 500
                    - font-size: 12px
                    - justify-self: start
                    - align-self: start
                    - margin-top: 2px
                    - color: var(--contrast10)
                  custom_fields:
                    connection:
                      - font-weight: 600
                      - font-size: 14px
                      - justify-self: end
                      - align-self: end
                      - margin-bottom: 2px
                    clients:
                      - font-weight: 400
                      - font-size: 12px
                      - justify-self: end
                      - align-self: start
                      - color: var(--contrast10)
                      - margin-top: 2px
                    arrow:
                      - color: var(--contrast10)
                    status_dot:
                      - margin-left: 7px
                      - align-self: center
                      - justify-self: center
                      - '--status-dot-color': var(--contrast8)
                custom_fields:
                  connection: |
                    [[[
                      if (entity.state === "home") {
                        return "Connected";
                      } else if (entity.state === "not_home") {
                        return "Not Connected";
                      } else {
                        return "Unknown";
                      }
                    ]]]
                  clients: |
                    [[[
                      var clients = states['sensor.cloud_gateway_ultra_clients'].state;
                      if (clients == null || isNaN(clients)) {
                        return "Unknown";
                      } else {
                        return clients + ' Clients';
                      }
                    ]]]
                  arrow: |
                    [[[
                      return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                    ]]]
                  status_dot: |
                    [[[
                      if (entity.state === 'home') {
                        return '<span style="width: 8px; height: 8px; background-color: green; border-radius: 50%; display: flex;"></span>';
                      } else {
                        return '<span style="width: 8px; height: 8px; background-color: red; border-radius: 50%; display: flex;"></span>';
                      }
                    ]]]
                state:
                  - value: home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': green
                  - value: not_home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': red
                tap_action:
                  action: navigate
                  navigation_path: /dashboard-home/cloud-gateway-ultra
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                name: BT Smart Hub 2
                entity_picture: /local/images/devices/bt_smart_hub_2.png
                label: HomeHub6DX
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 8px
                    - height: 56px
                    - padding-top: 0px
                    - padding-bottom: 0px
                  grid:
                    - grid-template-areas: |
                        "i n connection status_dot arrow" 
                        "i l clients status_dot arrow"
                    - grid-template-columns: 2fr 8fr 2fr 1fr 1fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 600
                    - font-size: 14px
                    - justify-self: start
                    - align-self: end
                    - margin-bottom: 2px
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 500
                    - font-size: 12px
                    - justify-self: start
                    - align-self: start
                    - margin-top: 2px
                    - color: var(--contrast10)
                  custom_fields:
                    connection:
                      - font-weight: 600
                      - font-size: 14px
                      - justify-self: end
                      - align-self: end
                      - margin-bottom: 2px
                    clients:
                      - font-weight: 400
                      - font-size: 12px
                      - justify-self: end
                      - align-self: start
                      - color: var(--contrast10)
                      - margin-top: 2px
                    arrow:
                      - color: var(--contrast10)
                    status_dot:
                      - margin-left: 7px
                      - align-self: center
                      - justify-self: center
                      - '--status-dot-color': var(--contrast8)
                custom_fields:
                  connection: |
                    [[[
                      if (states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state !== "0" || states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state !== "unavailable") {
                        return "Connected";
                      } else if (states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state > "1") {
                        return "Not Connected";
                      } else {
                        return "Unknown";
                      }
                    ]]]
                  clients: |
                    [[[
                      var clients = states['sensor.bt_smart_hub_2_online_devices'].state;
                      if (clients == null || isNaN(clients)) {
                        return "Unknown";
                      } else {
                        return clients + ' Clients';
                      }
                    ]]]
                  arrow: |
                    [[[
                      return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                    ]]]
                  status_dot: |
                    [[[
                      if (states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state !== "0" || states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state !== "unavailable") {
                        return '<span style="width: 8px; height: 8px; background-color: green; border-radius: 50%; display: flex;"></span>';
                      } else {
                        return '<span style="width: 8px; height: 8px; background-color: red; border-radius: 50%; display: flex;"></span>';
                      }
                    ]]]
                state:
                  - value: home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': green
                  - value: not_home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': red
                tap_action:
                  action: navigate
                  navigation_path: /dashboard-home/bt-smart-hub-2
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: device_tracker.kitchen_nighthawk_x6_r8000
                entity_picture: /local/images/devices/r8000.webp
                name: Nighthawk X6 R8000
                label: ‎R8000-100UKS
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 8px
                    - height: 56px
                    - padding-top: 0px
                    - padding-bottom: 0px
                  grid:
                    - grid-template-areas: |
                        "i n connection status_dot arrow" 
                        "i l clients status_dot arrow"
                    - grid-template-columns: 2fr 8fr 2fr 1fr 1fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 600
                    - font-size: 14px
                    - justify-self: start
                    - align-self: end
                    - margin-bottom: 2px
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 500
                    - font-size: 12px
                    - justify-self: start
                    - align-self: start
                    - margin-top: 2px
                    - color: var(--contrast10)
                  custom_fields:
                    connection:
                      - font-weight: 600
                      - font-size: 14px
                      - justify-self: end
                      - align-self: end
                      - margin-bottom: 2px
                    clients:
                      - font-weight: 400
                      - font-size: 12px
                      - justify-self: end
                      - align-self: start
                      - color: var(--contrast10)
                      - margin-top: 2px
                    arrow:
                      - color: var(--contrast10)
                    status_dot:
                      - margin-left: 7px
                      - align-self: center
                      - justify-self: center
                      - '--status-dot-color': var(--contrast8)
                custom_fields:
                  connection: |
                    [[[
                      if (entity.state === "home") {
                        return "Connected";
                      } else if (entity.state === "not_home") {
                        return "Not Connected";
                      } else {
                        return entity.state;
                      }
                    ]]]
                  clients: |
                    [[[
                      var clients = states['sensor.nighthawk_x6_r8000_wifi_devices'].state;
                      if (clients == null || isNaN(clients)) {
                        return "Unknown";
                      } else {
                        return states['sensor.nighthawk_x6_r8000_wifi_devices'].state + ' Clients';
                      }
                    ]]]
                  arrow: |
                    [[[
                      return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                    ]]]
                  status_dot: |
                    [[[
                      if (entity.state === 'home') {
                        return '<span style="width: 8px; height: 8px; background-color: green; border-radius: 50%; display: flex;"></span>';
                      } else {
                        return '<span style="width: 8px; height: 8px; background-color: red; border-radius: 50%; display: flex;"></span>';
                      }
                    ]]]
                state:
                  - value: home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': green
                  - value: not_home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': red
                tap_action:
                  action: navigate
                  navigation_path: /dashboard-home/nighthawk-x6-r8000
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: device_tracker.google_nest_wifi_pro_2
                entity_picture: /local/images/devices/Google_Nest_WIFI_Pro.png
                label: |
                  [[[
                    let state = states['sensor.google_nest_wifi_pro_model_id'].state;
                    return state.charAt(0).toUpperCase() + state.slice(1).toLowerCase();
                  ]]]
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 8px
                    - height: 56px
                    - padding-top: 0px
                    - padding-bottom: 0px
                  grid:
                    - grid-template-areas: |
                        "i n connection status_dot arrow" 
                        "i l clients status_dot arrow"
                    - grid-template-columns: 2fr 8fr 2fr 1fr 1fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 600
                    - font-size: 14px
                    - justify-self: start
                    - align-self: end
                    - margin-bottom: 2px
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 500
                    - font-size: 12px
                    - justify-self: start
                    - align-self: start
                    - margin-top: 2px
                    - color: var(--contrast10)
                  custom_fields:
                    connection:
                      - font-weight: 600
                      - font-size: 14px
                      - justify-self: end
                      - align-self: end
                      - margin-bottom: 2px
                    clients:
                      - font-weight: 400
                      - font-size: 12px
                      - justify-self: end
                      - align-self: start
                      - color: var(--contrast10)
                      - margin-top: 2px
                    arrow:
                      - color: var(--contrast10)
                    status_dot:
                      - margin-left: 7px
                      - align-self: center
                      - justify-self: center
                      - '--status-dot-color': var(--contrast8)
                custom_fields:
                  connection: |
                    [[[
                      if (entity.state === "home") {
                        return "Connected";
                      } else if (entity.state === "not_home") {
                        return "Not Connected";
                      } else {
                        return entity.state;
                      }
                    ]]]
                  clients: |
                    [[[
                      const unifiGatewayClients = parseInt(states['sensor.cloud_gateway_ultra_clients'].state, 10);
                      const btClients = parseInt(states['sensor.bt_smart_hub_2_online_devices'].state, 10);
                      const r8000Clients = parseInt(states['sensor.nighthawk_x6_r8000_wifi_devices'].state, 10);
                      
                      if (isNaN(btClients) || isNaN(r8000Clients) || isNaN(unifiGatewayClients)) {
                        return 'Unknown';
                      }

                      const googleClients = unifiGatewayClients - btClients - r8000Clients;
                      
                      if (googleClients >= 0) {
                        return googleClients + ' Clients';
                      }

                      return "Unknown";
                    ]]]
                  arrow: |
                    [[[
                      return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                    ]]]
                  status_dot: |
                    [[[
                      if (entity.state === 'home') {
                        return '<span style="width: 8px; height: 8px; background-color: green; border-radius: 50%; display: flex;"></span>';
                      } else {
                        return '<span style="width: 8px; height: 8px; background-color: red; border-radius: 50%; display: flex;"></span>';
                      }
                    ]]]
                state:
                  - value: home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': green
                  - value: not_home
                    styles:
                      custom_fields:
                        status_dot:
                          - '--status-dot-color': red
                tap_action:
                  action: navigate
                  navigation_path: /dashboard-home/google-nest-wifi-pro
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
      - type: custom:gap-card
        height: 32
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 18px 0px 0px 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: custom:button-card
            name: Clients
            show_name: true
            styles:
              card:
                - padding-top: 0px
                - padding-left: 18px
                - padding-right: 18px
                - padding-bottom: 18px
                - height: min-content
                - background-color: transparent
              name:
                - font-weight: 500
                - justify-self: start
                - align-self: end
                - padding-bottom: 3px
                - font-size: 1.5rem
          - type: custom:auto-entities
            sort:
              method: attribute
              attribute: ip
              ip: true
            card:
              type: entities
              card_mod:
                style: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                    padding: 0px;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 18px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            filter:
              include:
                - integration: unifi
                  attributes:
                    ip: '*'
                  options:
                    type: custom:button-card
                    show_name: true
                    show_label: true
                    show_icon: false
                    show_state: false
                    tap_action:
                      action: more-info
                    name: |
                      [[[ 
                        return entity.attributes.friendly_name;
                      ]]]
                    label: |
                      [[[ 
                        return entity.attributes.ip;
                      ]]]
                    styles:
                      card:
                        - padding: 0px
                        - border-radius: 0px
                        - margin: 0px
                        - background: transparent
                      grid:
                        - grid-template-areas: |
                            "divider divider divider"
                            "n l arrow"
                            "n mac arrow"
                        - grid-template-columns: 7fr 6fr 1fr
                        - grid-template-rows: min-content 35px 36px
                      name:
                        - padding-left: 18px
                        - justify-self: start
                        - font-weight: 500
                        - align-self: center
                        - font-size: 14px
                      label:
                        - padding-right: 18px
                        - justify-self: end
                        - color: var(--contrast10)
                        - align-self: end
                        - font-size: 12px
                        - margin: 0px 0px 2px 0px
                      custom_fields:
                        divider:
                          - padding: 0px
                          - margin: 0px
                        mac:
                          - color: var(--contrast10)
                          - justify-self: end
                          - align-self: start
                          - text-align: top
                          - font-size: 12px
                          - padding: 0px 18px 0px 0px
                          - margin: 2px 0px 0px 0px
                        arrow:
                          - color: var(--contrast10)
                          - padding-right: 0px
                    custom_fields:
                      mac: |
                        [[[ 
                          return entity.attributes.mac;
                        ]]]
                      arrow: |
                        [[[
                          return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                        ]]]
                      divider:
                        card:
                          type: entities
                          entities:
                            - type: divider
                          card_mod:
                            style: |
                              #states {
                                padding: 0px;
                                margin: 0px;
                              }
                              ha-card {
                                background-color: transparent;
                                box-shadow: none;
                                padding: 0px;
                              }
              card_mod:
                style: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                    padding: 0px;
                  }
    type: custom:vertical-layout
  - title: BT Smart Hub 2
    path: bt-smart-hub-2
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity_picture: /local/images/devices/bt_smart_hub_2.png
                name: BT Smart Hub 2
                label: HomeHub6DX
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 0px
                    - height: 150px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: HomeHub6DX
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.darron
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      let uptime = parseInt(states['sensor.bt_smart_hub_2_system_uptime_in_seconds'].state, 10);
                      let days = Math.floor(uptime / (24 * 60 * 60));
                      let hours = Math.floor((uptime % (24 * 60 * 60)) / (60 * 60));
                      let minutes = Math.floor((uptime % (60 * 60)) / 60);
                      return `${days}d ${hours}h ${minutes}m`;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Firmware Version
                  val: |
                    [[[
                      const with_date = states['sensor.bt_smart_hub_2_firmware_version'].state;
                      const no_date = with_date.split(' ')[0];
                      return no_date;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: custom:button-card
                custom_fields:
                  title: Last Firmware Update
                  val: |
                    [[[
                      let timestamp = states['sensor.bt_smart_hub_2_firmware_update_time'].state;
                      let date = new Date(parseInt(timestamp));
                      let year = date.getFullYear();
                      let month = ('0' + (date.getMonth() + 1)).slice(-2);
                      let day = ('0' + date.getDate()).slice(-2);
                      let hours = ('0' + date.getHours()).slice(-2);
                      let minutes = ('0' + date.getMinutes()).slice(-2);
                      return `${year}-${month}-${day} ${hours}:${minutes}`;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Serial Number
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_serial_number'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Download Traffic
                  val: |
                    [[[
                      let bytes = parseFloat(states['sensor.bt_smart_hub_2_wan_download_traffic'].state);
                      let gigabytes = bytes / (1024 * 1024 * 1024);
                      return gigabytes.toFixed(2) + ' GB';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Download Traffic
                  val: |
                    [[[
                      let bytes = parseFloat(states['sensor.bt_smart_hub_2_wan_upload_traffic'].state);
                      let gigabytes = bytes / (1024 * 1024 * 1024);
                      return gigabytes.toFixed(2) + ' GB';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Total Traffic
                  val: |
                    [[[
                      let bytes = parseFloat(states['sensor.bt_smart_hub_2_wan_total_traffic'].state);
                      let gigabytes = bytes / (1024 * 1024 * 1024);
                      return gigabytes.toFixed(2) + ' GB';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Public IPv4 Address
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_ipv4_public_address'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Primary IPv4 DNS Address
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_ipv4_primary_dns'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Secondary IPv4 DNS Address
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_ipv4_primary_dns'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Secondary IPv4 DNS Address
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_ipv4_subnet_mask'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Default IPv4 Gateway Address
                  val: |
                    [[[
                      return states['sensor.bt_smart_hub_2_ipv4_subnet_mask'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
    subview: true
    type: custom:vertical-layout
  - title: Nighthawk X6 R8000
    path: nighthawk-x6-r8000
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity: device_tracker.kitchen_nighthawk_x6_r8000
                entity_picture: /local/images/devices/r8000.webp
                label: ‎R8000-100UKS
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 0px
                    - height: 150px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: ‎R8000-100UKS
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.james
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      function formatDuration(lastTime) {
                        const now = new Date();
                        const last = new Date(lastTime);
                        const diff = Math.abs(now - last);
                        
                        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                        const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                        const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                        
                        return `${days}d ${hours}h ${minutes}m`;
                      }
                      
                      return formatDuration(states['device_tracker.kitchen_nighthawk_x6_r8000'].attributes['last_time_reachable']);
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Firmware Version
                  val: >
                    [[[ return
                    states['update.nighthawk_x6_r8000_firmware'].attributes.installed_version;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Wifi Clients
                  val: >
                    [[[ return
                    states['sensor.nighthawk_x6_r8000_wifi_devices'].state; ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: CPU Utilisation
                  val: >
                    [[[ return
                    states['sensor.nighthawk_x6_r8000_cpu_utilization'].state +
                    ' %'; ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Memory Utilisation
                  val: >
                    [[[ return
                    states['sensor.nighthawk_x6_r8000_memory_utilization'].state
                    + ' %'; ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
    subview: true
    type: custom:vertical-layout
  - title: Google Nest Wifi Pro
    path: google-nest-wifi-pro
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity: device_tracker.google_nest_wifi_pro_2
                entity_picture: /local/images/devices/Google_Nest_WIFI_Pro.png
                label: |
                  [[[
                    let state = states['sensor.google_nest_wifi_pro_model_id'].state;
                    return state.charAt(0).toUpperCase() + state.slice(1).toLowerCase();
                  ]]]
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 0px
                    - height: 150px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: |
                    [[[
                      let state = states['sensor.google_nest_wifi_pro_model_id'].state;
                      return state.charAt(0).toUpperCase() + state.slice(1).toLowerCase();
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.james
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      let seconds = states['sensor.google_nest_wifi_pro_uptime_2'].state;
                      let days = Math.floor(seconds / (24 * 3600));
                      seconds %= (24 * 3600);
                      let hours = Math.floor(seconds / 3600);
                      seconds %= 3600;
                      let minutes = Math.floor(seconds / 60);
                      return `${days}d ${hours}h ${minutes}m`;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Firmware Version
                  val: |
                    [[[ 
                      return states['sensor.google_nest_wifi_pro_software_version'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: LED Brightness
                  val: >
                    [[[ return
                    states['sensor.google_nest_wifi_pro_led_brightness'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Link Type
                  val: |
                    [[[ 
                      var linkType = states['sensor.google_nest_wifi_pro_link_type'].state;
                      return linkType.charAt(0).toUpperCase() + linkType.slice(1);
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Local IPv4 Address
                  val: >
                    [[[ return
                    states['sensor.google_nest_wifi_pro_wan_local_ipv4_address'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Gateway IPv4 Address
                  val: >
                    [[[ return
                    states['sensor.google_nest_wifi_pro_wan_gateway_ipv4_address'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: '"title val"'
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                    }
    subview: true
    type: custom:vertical-layout
  - title: Cloud Gateway Ultra
    path: cloud-gateway-ultra
    type: custom:vertical-layout
    subview: true
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity: device_tracker.cloud_gateway_ultra
                entity_picture: /local/images/devices/UCG_Ultra.png
                label: UCG Ultra
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 0px
                    - height: 150px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: start
                    - width: 100%
                    - height: 100%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: UCG Ultra
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.james
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      const startTime = new Date(states['sensor.cloud_gateway_ultra_uptime'].state);
                      const now = new Date();
                      const diff = now - startTime;

                      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                      const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));

                      return `${days}d ${hours}h ${minutes}m`;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Firmware Version
                  val: |
                    [[[
                      return states['update.cloud_gateway_ultra'].attributes.installed_version;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Link Type
                  val: |
                    [[[ 
                      var linkType = states['sensor.google_nest_wifi_pro_link_type'].state;
                      return linkType.charAt(0).toUpperCase() + linkType.slice(1);
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Online Clients
                  val: |
                    [[[ 
                      return states['sensor.cloud_gateway_ultra_clients'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: CPU Utilisation
                  val: |
                    [[[
                      return states['sensor.cloud_gateway_ultra_cpu_utilization'].state + ' %';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: CPU Utilisation
                  val: |
                    [[[
                      return states['sensor.cloud_gateway_ultra_memory_utilization'].state + ' %';
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
  - title: Bambu Lab P1S
    path: bambu-lab-p1s
    type: custom:vertical-layout
    subview: true
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:stack-in-card
        card_mod:
          style:
            .: |
              ha-card {
                background-color: transparent;
                box-shadow: none;
                padding: 0px !important;
                margin: 0px !important;
                border-radius: 0px;
              }
        cards:
          - type: entities
            card_mod:
              style:
                .: |
                  ha-card {
                    background-color: transparent;
                    box-shadow: none;
                  }
                  #states {
                    padding-top: 0px !important;
                    padding-left: 0px !important;
                    padding-right: 0px !important;
                    padding-bottom: 0px !important;
                  }
                  #states > div {
                    margin-top: 0px !important;
                    margin-bottom: 0px !important;
                    margin-left: 0px !important;
                    margin-right: 0px !important;
                  }
            entities:
              - type: custom:button-card
                entity: device_tracker.james_bambu_lab_p1s
                entity_picture: /local/images/devices/Bambu_Lab_P1S.png
                name: |
                  [[[
                    return states['sensor.james_bambu_lab_p1s_printer_name'].state;
                  ]]]
                label: Bambu Lab P1S
                show_label: true
                show_name: true
                show_icon: false
                show_state: false
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 0px
                    - padding-bottom: 0px
                    - height: 150px
                    - background-color: transparent
                  grid:
                    - grid-template-areas: |
                        "i n" 
                        "i l"
                    - grid-template-columns: 1fr 2fr
                    - grid-template-rows: 1fr 1fr
                  name:
                    - font-weight: 500
                    - justify-self: start
                    - align-self: end
                    - padding-bottom: 3px
                    - font-size: 1.5rem
                  img_cell:
                    - justify-content: start
                    - width: 80%
                    - height: 80%
                  icon:
                    - width: 70%
                  label:
                    - font-weight: 400
                    - justify-self: start
                    - align-self: start
                    - padding-top: 3px
                    - color: var(--contrast10)
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Model
                  val: P1S
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                entity: person.james
                show_name: true
                show_label: false
                show_icon: true
                custom_fields:
                  title: Owner
                show_entity_picture: true
                styles:
                  card:
                    - padding-left: 18px
                    - padding-right: 18px
                    - padding-top: 9px
                    - padding-bottom: 9px
                  grid:
                    - grid-template-areas: |
                        "title i n"
                  img_cell:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                  icon:
                    - justify-self: end
                    - padding: 0px
                    - margin: 0px
                    - height: 38px
                    - width: 38px
                    - border-radius: 50%
                  name:
                    - padding-left: 12px
                    - color: var(--contrast10)
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Uptime
                  val: |
                    [[[
                      const startTime = new Date("2024-07-10T07:47:24+00:00");
                      const now = new Date();
                      const diff = now - startTime;

                      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                      const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));

                      return `${days}d ${hours}h ${minutes}m`;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
              - type: custom:button-card
                custom_fields:
                  title: Firmware Version
                  val: |
                    [[[
                      return states['sensor.james_bambu_lab_p1s_firmware_version'].state;
                    ]]]
                styles:
                  card:
                    - padding: 18px
                  grid:
                    - grid-template-areas: |
                        "title val"
                  custom_fields:
                    title:
                      - justify-self: start
                      - font-weight: 500
                    val:
                      - justify-self: end
                      - color: var(--contrast10)
                card_mod:
                  style:
                    .: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                      }
              - type: divider
      - type: conditional
        conditions:
          - condition: state
            entity: sensor.james_bambu_lab_p1s_print_progress
            state_not: '0'
        card:
          type: vertical-stack
          cards:
            - type: custom:gap-card
              height: 36
            - type: picture
              image_entity: image.james_bambu_lab_p1s_camera
              hold_action:
                action: more-info
              tap_action:
                action: more-info
            - type: custom:gap-card
              height: 16
            - type: horizontal-stack
              cards:
                - type: custom:bar-card
                  name: Progress
                  color: '#00bb33'
                  max: 100
                  positions:
                    name: outside
                    icon: 'off'
                    value: 'off'
                    indicator: 'off'
                  unit_of_measurement: '%'
                  width: 80%
                  entities:
                    - entity: sensor.james_bambu_lab_p1s_print_progress
                  entity_row: true
                - type: custom:button-card
                  entity: sensor.james_bambu_lab_p1s_print_progress
                  show_name: false
                  show_label: false
                  show_state: true
                  show_icon: false
                  styles:
                    card:
                      - width: max-content
                      - height: 100%
                      - padding-left: 10px
                    state:
                      - font-size: 14px
                      - padding: 14px
                    custom_fields:
                      state:
                        - color: '#00bb33'
                  card_mod:
                    style: |
                      ha-card {
                        background-color: transparent;
                        box-shadow: none;
                        padding: 0px !important;
                        margin: 0px !important;
                        border-radius: 0px;
                      }
            - type: custom:gap-card
              height: 8
            - square: false
              type: grid
              cards:
                - type: custom:mini-graph-card
                  name: Nozzle Temperature
                  entities:
                    - entity: sensor.james_bambu_lab_p1s_nozzle_target_temperature
                      name: Target
                      color: '#2196f3'
                      show_state: true
                      show_indicator: false
                    - entity: sensor.james_bambu_lab_p1s_nozzle_temperature
                      name: Actual
                      color: '#00bb33'
                      show_state: true
                      show_indicator: false
                  hours_to_show: 12
                  line_width: 3
                  font_size: 100
                  animate: true
                  show:
                    name: true
                    icon: false
                    labels: false
                    labels_secondary: true
                    legend: true
                    fill: fade
                    points: true
                  card_mod:
                    style: |
                      ha-card {
                        background: transparent !important;
                        box-shadow: none !important;
                      }
                - type: custom:mini-graph-card
                  name: Bed Temperature
                  entities:
                    - entity: sensor.james_bambu_lab_p1s_target_bed_temperature
                      name: Target
                      color: '#2196f3'
                      show_state: true
                      show_indicator: false
                    - entity: sensor.james_bambu_lab_p1s_bed_temperature
                      name: Actual
                      color: '#00bb33'
                      show_state: true
                      show_indicator: false
                  hours_to_show: 12
                  line_width: 3
                  font_size: 100
                  animate: true
                  show:
                    name: true
                    icon: false
                    labels: false
                    labels_secondary: true
                    legend: true
                    fill: fade
                    points: true
                  card_mod:
                    style: |
                      ha-card {
                        background: transparent !important;
                        box-shadow: none !important;
                      }
              columns: 2
            - type: custom:gap-card
              height: 8
            - type: custom:auto-entities
              sort:
                method: friendly_name
              card:
                type: entities
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                      padding: 0px;
                    }
                    #states {
                      padding-top: 18px !important;
                      padding-left: 0px !important;
                      padding-right: 0px !important;
                      padding-bottom: 18px !important;
                    }
                    #states > div {
                      margin-top: 0px !important;
                      margin-bottom: 0px !important;
                      margin-left: 0px !important;
                      margin-right: 0px !important;
                    }
              filter:
                exclude:
                  - entity_id: image.*
                  - entity_id: device_tracker.james_bambu_lab_p1s
                  - entity_id: sensor.*temperature*
                  - entity_id: sensor.james_bambu_lab_p1s_printer_name
                  - entity_id: sensor.james_bambu_lab_p1s_print_progress
                include:
                  - device: James' Bambu Lab P1S
                    options:
                      type: custom:button-card
                      show_name: true
                      show_label: false
                      show_icon: false
                      show_state: true
                      tap_action:
                        action: more-info
                      name: |
                        [[[ 
                          return entity.attributes.friendly_name;
                        ]]]
                      label: |
                        [[[ 
                          return entity.attributes.ip;
                        ]]]
                      styles:
                        card:
                          - padding: 0px
                          - border-radius: 0px
                          - margin: 0px
                          - background: transparent
                        grid:
                          - grid-template-areas: |
                              "divider divider divider"
                              "n s arrow"
                              "n s arrow"
                          - grid-template-columns: 8fr 5fr 1fr
                          - grid-template-rows: min-content 35px 36px
                        name:
                          - padding-left: 18px
                          - justify-self: start
                          - font-weight: 500
                          - font-size: 14px
                          - align-self: center
                          - text-align: left
                          - white-space: normal
                          - word-wrap: break-word
                          - overflow: hidden
                        state:
                          - padding-right: 18px
                          - justify-self: end
                          - color: var(--contrast10)
                          - align-self: center
                          - margin: 0px 0px 2px 0px
                          - text-align: right
                          - white-space: normal
                          - word-wrap: break-word
                          - overflow: hidden
                          - font-size: 14px
                        custom_fields:
                          divider:
                            - padding: 0px
                            - margin: 0px
                          arrow:
                            - color: var(--contrast10)
                            - padding-right: 0px
                      custom_fields:
                        arrow: |
                          [[[
                            return '<ha-icon icon="mdi:chevron-right"></ha-icon>';
                          ]]]
                        divider:
                          card:
                            type: entities
                            entities:
                              - type: divider
                            card_mod:
                              style: |
                                #states {
                                  padding: 0px;
                                  margin: 0px;
                                }
                                ha-card {
                                  background-color: transparent;
                                  box-shadow: none;
                                  padding: 0px;
                                }
                card_mod:
                  style: |
                    ha-card {
                      background-color: transparent;
                      box-shadow: none;
                      padding: 0px;
                    }
  - title: Device Tracker
    path: device-tracker
    type: custom:vertical-layout
    subview: true
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:auto-entities
        card:
          type: entities
          state_color: true
          show_header_toggle: false
        filter:
          include:
            - domain: device_tracker
          exclude:
            - template: |
                {{ is_state_attr(this.entity_id, 'source', 'Unknown') or
                   is_state_attr(this.entity_id, 'source', None) or
                   is_state_attr(this.entity_id, 'source', null) or
                   is_state_attr(this.entity_id, 'source', '') or
                   is_state_attr(this.entity_id, 'source', '0') }}
        sort:
          method: state
  - title: Living Room TV
    path: living-room-tv
    cards:
      - type: custom:mushroom-chips-card
        chips:
          - type: back
            card_mod:
              style: |
                ha-card {
                  background: transparent;
                  --chip-background: transparent;
                  box-shadow: none;
                  margin: 18px 0px 18px 0px;
                }
      - type: custom:mushroom-media-player-card
        entity: media_player.living_room_tv
        fill_container: true
        icon_type: entity-picture
        use_media_info: true
        show_volume_level: true
        volume_controls:
          - volume_mute
          - volume_set
          - volume_buttons
        media_controls:
          - on_off
        collapsible_controls: true
        tap_action:
          action: more-info
        hold_action:
          action: more-info
        double_tap_action:
          action: more-info
      - type: custom:mushroom-media-player-card
        fill_container: true
        icon_type: entity-picture
        use_media_info: true
        show_volume_level: true
        volume_controls:
          - volume_mute
          - volume_set
          - volume_buttons
        media_controls:
          - on_off
        collapsible_controls: true
        tap_action:
          action: more-info
        hold_action:
          action: more-info
        double_tap_action:
          action: more-info
        entity: media_player.tv_samsung_7_series_55
      - type: custom:gap-card
        height: 32
      - type: custom:auto-entities
        card:
          type: entities
        filter:
          include:
            - area: Living Room
        sort:
          method: friendly_name
    subview: true
    type: custom:vertical-layout
```
<br>

</details>

<br>

# Animated Assistant

It is based on a recording of a codepen located here:  [https://codepen.io/tuckermassad/pen/yLNOPrO](https://codepen.io/tuckermassad/pen/yLNOPrO)

I edited it to the following:

<details>
<summary>chatbot.html</summary>

```
<!DOCTYPE html>
<html>

<head>
    <style>
        :root {
            --assistant-color: white;
            --assistant-bg: #111318;
            --width: 200 /* px */;

            /* Calculations */
            --scaler: calc(var(--width) / 200);
        }

        html,
        body {
            height: 100%;
            width: 100%;
            margin: 0;
            overflow: hidden;
            background-color: var(--assistant-bg);
        }

        .assistant-container {
            margin: auto;
            position: absolute;
            bottom: 0;
            left: 0;
            top: 0;
            right: 0;
            height: calc(200px * var(--scaler));
            width: calc(200px * var(--scaler));
            animation: up-down 7.5s infinite ease-in-out;
            background-color: var(--assistant-bg);
        }

        .assistant-container #assistant {
            margin: auto;
            position: absolute;
            bottom: 0;
            left: 0;
            top: 0;
            right: 0;
            width: calc(150px * var(--scaler));
            height: calc(85px * var(--scaler));
            border: calc(12px * var(--scaler)) solid var(--assistant-color);
            border-radius: 5rem;
        }

        .assistant-container #assistant-corner {
            margin: auto;
            position: absolute;
            bottom: 0;
            left: 0;
            top: 0;
            right: 0;
            top: calc(105px * var(--scaler));
            left: calc(-65px * var(--scaler));
            width: 0;
            height: 0;
            border-left: calc(20px * var(--scaler)) solid transparent;
            border-right: calc(20px * var(--scaler)) solid transparent;
            border-top: calc(25px * var(--scaler)) solid var(--assistant-color);
            transform: rotate(140deg);
        }

        .assistant-container #assistant-antenna {
            margin: auto;
            position: absolute;
            bottom: 0;
            left: 0;
            top: 0;
            right: 0;
            top: calc(-125px * var(--scaler));
            height: calc(20px * var(--scaler));
            width: calc(10px * var(--scaler));
            background-color: var(--assistant-color);
            animation: antenna-appear 7.5s infinite ease-in-out;
        }

        .assistant-container #assistant-antenna #assistant-beam {
            position: absolute;
            top: calc(-12.5px * var(--scaler));
            left: calc(-5px * var(--scaler));
            height: calc(20px * var(--scaler));
            width: calc(20px * var(--scaler));
            border-radius: 50%;
            background-color: var(--assistant-color);
            animation: beam-appear 7.5s infinite ease-in-out;
        }

        .assistant-container #assistant-antenna #assistant-beam-pulsar {
            position: absolute;
            top: calc(-12.5px * var(--scaler));
            left: calc(-5px * var(--scaler));
            height: calc(20px * var(--scaler));
            width: calc(20px * var(--scaler));
            border-radius: 50%;
            background-color: var(--assistant-color);
            animation: beam-pulsar-appear 7.5s infinite ease-in-out;
        }

        .assistant-container .assistant-dot {
            height: calc(17.5px * var(--scaler));
            width: calc(17.5px * var(--scaler));
            margin: auto;
            position: absolute;
            bottom: 0;
            left: 0;
            top: 0;
            right: 0;
            left: calc(-65px * var(--scaler));
            background-color: var(--assistant-color);
            border-radius: 50%;
            animation: pulse-outer 7.5s infinite ease-in-out;
        }

        .assistant-container .assistant-dot:nth-child(2) {
            left: 0;
            animation: pulse-inner 7.5s infinite ease-in-out;
            animation-delay: 0.2s;
        }

        .assistant-container .assistant-dot:nth-child(3) {
            left: calc(65px * var(--scaler));
            animation: pulse-outer 7.5s infinite ease-in-out;
            animation-delay: 0.4s;
        }

        @keyframes pulse-inner {
            0% {
                transform: scale(1);
            }

            7.5% {
                transform: scale(1.5);
            }

            15% {
                transform: scale(1);
            }

            22.5% {
                transform: scale(1.5);
            }

            30% {
                transform: scale(1);
            }

            37.5% {
                transform: scale(1.5);
            }

            45% {
                top: 0;
                transform: scale(1);
                height: calc(17.5px * var(--scaler));
                border-bottom-left-radius: 50%;
                border-bottom-right-radius: 50%;
                transform: rotate(-370deg);
            }

            50% {
                top: calc(22.5px * var(--scaler));
                height: calc(10px * var(--scaler));
                border-top-left-radius: 50%;
                border-top-right-radius: 50%;
                border-bottom-left-radius: 3rem;
                border-bottom-right-radius: 3rem;
                transform: rotate(10deg);
            }

            55% {
                transform: rotate(-10deg);
            }

            60% {
                transform: rotate(10deg);
            }

            65% {
                transform: rotate(-10deg);
            }

            65% {
                transform: rotate(0deg);
            }

            85% {
                top: calc(22.5px * var(--scaler));
                height: calc(10px * var(--scaler));
                border-top-left-radius: 50%;
                border-top-right-radius: 50%;
                border-bottom-left-radius: 3rem;
                border-bottom-right-radius: 3rem;
                transform: rotate(0deg);
            }

            92.5% {
                top: calc(22.5px * var(--scaler));
                height: calc(10px * var(--scaler));
                border-top-left-radius: 50%;
                border-top-right-radius: 50%;
                border-bottom-left-radius: 2.5rem;
                border-bottom-right-radius: 2.5rem;
                transform: rotate(0deg);
            }

            100% {
                top: 0;
                height: calc(17.5px * var(--scaler));
                border-radius: 50%;
                transform: rotate(-360deg);
            }
        }

        @keyframes pulse-outer {
            0% {
                transform: scale(1);
            }

            7.5% {
                transform: scale(1.5);
            }

            15% {
                transform: scale(1);
            }

            22.5% {
                transform: scale(1.5);
            }

            30% {
                transform: scale(1);
            }

            37.5% {
                transform: scale(1.5);
            }

            45% {
                transform: scale(1);
                height: calc(17.5px * var(--scaler));
            }

            55% {
                tranform: scale(1);
                height: calc(5px * var(--scaler));
            }

            60% {
                height: calc(17.5px * var(--scaler));
            }

            75% {
                height: calc(17.5px * var(--scaler));
            }

            80% {
                tranform: scale(1);
                height: calc(5px * var(--scaler));
            }

            85% {
                height: calc(17.5px * var(--scaler));
            }

            100% {
                height: calc(17.5px * var(--scaler));
            }
        }

        @keyframes antenna-appear {
            0% {
                visibility: hidden;
                top: calc(-100px * var(--scaler));
                height: 0;
            }

            50% {
                visibility: hidden;
                top: calc(-100px * var(--scaler));
                height: 0;
            }

            55% {
                visibility: visible;
                top: calc(-125px * var(--scaler));
                height: calc(20px * var(--scaler));
            }

            95% {
                visibility: visible;
                top: calc(-125px * var(--scaler));
                height: calc(20px * var(--scaler));
            }

            100% {
                top: calc(-100px * var(--scaler));
                height: 0;
            }
        }

        @keyframes beam-appear {
            0% {
                visibility: hidden;
                top: calc(-12.5px * var(--scaler));
                height: 0;
            }

            50% {
                visibility: hidden;
                top: calc(-12.5px * var(--scaler));
                height: 0;
            }

            55% {
                visibility: visible;
                top: calc(-12.5px * var(--scaler));
                height: calc(20px * var(--scaler));
                width: calc(20px * var(--scaler));
            }

            100% {
                visibility: visible;
                top: calc(-12.5px * var(--scaler));
                height: calc(20px * var(--scaler));
                width: calc(20px * var(--scaler));
            }
        }

        @keyframes beam-pulsar-appear {
            0% {
                visibility: hidden;
                top: calc(-12.5px * var(--scaler));
                height: 0;
            }

            50% {
                visibility: hidden;
                top: calc(-12.5px * var(--scaler));
                height: 0;
            }

            55% {
                visibility: visible;
                top: calc(-12.5px * var(--scaler));
                left: calc(-5px * var(--scaler));
                height: calc(20px * var(--scaler));
                width: cal(20px * var(--scaler));
                opacity: 1;
            }

            65% {
                top: calc(-25px * var(--scaler));
                left: calc(-15px * var(--scaler));
                height: calc(40px * var(--scaler));
                width: calc(40px * var(--scaler));
                opacity: 0;
                visibility: visible;
            }

            74% {
                visibility: hidden;
                opacity: 0;
            }

            75% {
                visibility: visible;
                top: calc(-12.5px * var(--scaler));
                left: calc(-5px * var(--scaler));
                height: calc(20px * var(--scaler));
                width: calc(20px * var(--scaler));
                opacity: 1;
            }

            85% {
                top: calc(-25px * var(--scaler));
                left: calc(-15px * var(--scaler));
                height: calc(40px * var(--scaler));
                width: calc(40px * var(--scaler));
                opacity: 0;
                visibility: visible;
            }

            94% {
                visibility: hidden;
                opacity: 0;
            }

            100% {
                visibility: hidden;
                opacity: 0;
            }
        }

        @keyframes up-down {
            0% {
                transform: translate(0);
            }

            2.5% {
                transform: translate(0, 2%);
            }

            25% {
                transform: translate(0);
            }

            37.5% {
                transform: translate(0, 2%);
            }

            50% {
                transform: translate(0);
            }

            62.5% {
                transform: translate(0, 2%);
            }

            75% {
                transform: translate(0);
            }

            87.5% {
                transform: translate(0, 2%);
            }

            100% {
                transform: translate(0);
            }
        }
    </style>
</head>

    <div class="assistant-container">
        <div id="assistant">
            <div class="assistant-dot"></div>
            <div class="assistant-dot"></div>
            <div class="assistant-dot"></div>
        </div>
        <div id="assistant-corner"></div>
        <div id="assistant-antenna">
            <div id="assistant-beam"></div>
            <div id="assistant-beam-pulsar"></div>
        </div>
    </div>

</html>
```
<br>

</details>

<br>

It was recorded using [OBS Studio](https://obsproject.com/). Trimmed to the same point in the animation, so one loop was completed. It was exported as `untitled.mkv`.

This was then converted to the image using the [FFmpeg](https://www.ffmpeg.org/download.html) command:

```
ffmpeg -i untitled.mkv -vf "crop=700:700:(in_w-700)/2:(in_h-700)/2, fps=60" -loop 0 -quality 100 -compression_level 0 -y chatbot_700x700.webp

```

This resulted in the image located here: [chatbot_700x700.webp](https://github.com/beecho01/homeassistant-setup/blob/main/www/Chatbot/chatbot_700x700.webp)

<br>

# Device Images

These can be found here: [devices](https://github.com/beecho01/homeassistant-setup/tree/main/www/images/devices)

<br>
Hope this helps!
<br>
beecho01
