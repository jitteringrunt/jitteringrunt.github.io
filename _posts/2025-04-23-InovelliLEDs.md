---
title: Inovelli Node-Red Individual LED Flow
date: 2025-04-23
categories: [Home Assistant, Node-Red]
tags: [homeassistant, nodered]     # TAG names should always be lowercase
---

Node-Red Flow to pull three different Home Assistant door sensor status into the individual Inovelli switch LEDs.  JSON is being sent to Inovelli switch via MQTT.

Use https://nathanfiscus.github.io/inovelli-notification-calc/ for your color values.

Additional nodes are added in disabled state to add additional segments if desired.

Inovelli Switch Images

![Screenshot 2025-04-16 091135](https://github.com/user-attachments/assets/ba59dab3-1412-4a97-938f-6d814bdcccf3)
No Doors Open
![PXL_20250416_130856567](https://github.com/user-attachments/assets/58bb0825-0b51-4cfe-ba35-08fb19b8fc5b)
One Door Open
![PXL_20250416_130910509](https://github.com/user-attachments/assets/32548826-e163-46a7-ac37-49b8f7421f7f)
Two Doors Open
![PXL_20250416_130945081](https://github.com/user-attachments/assets/fc7bf0b7-c248-4c6e-8de7-cb68115f761d)
Three Doors Open
![PXL_20250416_130958041](https://github.com/user-attachments/assets/925a6db7-c00e-463b-9b38-b5414cbd8ca0)

Flow Code:
```
[
    {
        "id": "52473e36c384202c",
        "type": "mqtt out",
        "z": "f06fe9656a6a47ec",
        "name": "",
        "topic": "zigbee2mqtt/Kitchen Table Light Switch/set",
        "qos": "",
        "retain": "",
        "respTopic": "",
        "contentType": "",
        "userProps": "",
        "correl": "",
        "expiry": "",
        "broker": "c75c14767a4d4681",
        "x": 1250,
        "y": 360,
        "wires": []
    },
    {
        "id": "8d9ff60b62e4d240",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "top_light_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":1,\"effect\":\"solid\",\"color\":0,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 790,
        "y": 140,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "61cd4b0e47d8c72f",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "d": true,
        "name": "bottom_light_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":5,\"effect\":\"solid\",\"color\":88,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 800,
        "y": 460,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "61073cf5eba2c792",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "d": true,
        "name": "middle_light_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":3,\"effect\":\"solid\",\"color\":198,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 800,
        "y": 300,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "dbefeb6a13f0f020",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "d": true,
        "name": "top_light_2",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":2,\"effect\":\"solid\",\"color\":0,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 790,
        "y": 220,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "4c002dac4cbdc3a1",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "middle_light_2",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":4,\"effect\":\"solid\",\"color\":198,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 800,
        "y": 380,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "7e87df4083e5c931",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "bottom_light_2",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":6,\"effect\":\"solid\",\"color\":88,\"level\":100,\"duration\":255}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 800,
        "y": 540,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "f80111e1b8ae6126",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "top_light_clear_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":1,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 810,
        "y": 180,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "8aa1952781152b36",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "top_light_clear_2",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":2,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 810,
        "y": 260,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "1aa325f70da6d955",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "middle_light_clear_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":3,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 820,
        "y": 340,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "e7310724f69736a9",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "middle_light_clear_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":4,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 820,
        "y": 420,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "d9be0d802778b13b",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "bottom_light_clear_1",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":5,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 820,
        "y": 500,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "91ceb2852c097e82",
        "type": "change",
        "z": "f06fe9656a6a47ec",
        "name": "bottom_light_clear_2",
        "rules": [
            {
                "t": "delete",
                "p": "topic",
                "pt": "msg"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{\"individual_led_effect\":{\"led\":6,\"effect\":\"clear_effect\"}}",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 820,
        "y": 580,
        "wires": [
            [
                "52473e36c384202c"
            ]
        ]
    },
    {
        "id": "7a10215dff23dbf7",
        "type": "trigger-state",
        "z": "f06fe9656a6a47ec",
        "name": "",
        "server": "f0f882f3.13a8c",
        "version": 5,
        "inputs": 0,
        "outputs": 2,
        "exposeAsEntityConfig": "",
        "entities": {
            "entity": [
                "binary_sensor.kitchen_door_sensor_contact"
            ],
            "substring": [],
            "regex": []
        },
        "debugEnabled": false,
        "constraints": [
            {
                "targetType": "this_entity",
                "targetValue": "",
                "propertyType": "current_state",
                "propertyValue": "new_state.state",
                "comparatorType": "is",
                "comparatorValueDatatype": "str",
                "comparatorValue": "on"
            }
        ],
        "customOutputs": [],
        "outputInitially": false,
        "stateType": "str",
        "enableInput": false,
        "x": 350,
        "y": 200,
        "wires": [
            [
                "8d9ff60b62e4d240",
                "dbefeb6a13f0f020"
            ],
            [
                "f80111e1b8ae6126",
                "8aa1952781152b36"
            ]
        ]
    },
    {
        "id": "bd1efea3d6d51a34",
        "type": "trigger-state",
        "z": "f06fe9656a6a47ec",
        "name": "",
        "server": "f0f882f3.13a8c",
        "version": 5,
        "inputs": 0,
        "outputs": 2,
        "exposeAsEntityConfig": "",
        "entities": {
            "entity": [
                "binary_sensor.laundry_room_door_sensor_contact"
            ],
            "substring": [],
            "regex": []
        },
        "debugEnabled": false,
        "constraints": [
            {
                "targetType": "this_entity",
                "targetValue": "",
                "propertyType": "current_state",
                "propertyValue": "new_state.state",
                "comparatorType": "is",
                "comparatorValueDatatype": "str",
                "comparatorValue": "on"
            }
        ],
        "customOutputs": [],
        "outputInitially": false,
        "stateType": "str",
        "enableInput": false,
        "x": 370,
        "y": 520,
        "wires": [
            [
                "61cd4b0e47d8c72f",
                "7e87df4083e5c931"
            ],
            [
                "d9be0d802778b13b",
                "91ceb2852c097e82"
            ]
        ]
    },
    {
        "id": "bee4f95fcf49076a",
        "type": "trigger-state",
        "z": "f06fe9656a6a47ec",
        "name": "",
        "server": "f0f882f3.13a8c",
        "version": 5,
        "inputs": 0,
        "outputs": 2,
        "exposeAsEntityConfig": "",
        "entities": {
            "entity": [
                "binary_sensor.living_room_door_sensor_contact"
            ],
            "substring": [],
            "regex": []
        },
        "debugEnabled": false,
        "constraints": [
            {
                "targetType": "this_entity",
                "targetValue": "",
                "propertyType": "current_state",
                "propertyValue": "new_state.state",
                "comparatorType": "is",
                "comparatorValueDatatype": "str",
                "comparatorValue": "on"
            }
        ],
        "customOutputs": [],
        "outputInitially": false,
        "stateType": "str",
        "enableInput": false,
        "x": 360,
        "y": 360,
        "wires": [
            [
                "61073cf5eba2c792",
                "4c002dac4cbdc3a1"
            ],
            [
                "1aa325f70da6d955",
                "e7310724f69736a9"
            ]
        ]
    },
    {
        "id": "c75c14767a4d4681",
        "type": "mqtt-broker",
        "name": "",
        "broker": "ADD BROKER IP",
        "port": "1883",
        "clientid": "",
        "autoConnect": true,
        "usetls": false,
        "protocolVersion": "4",
        "keepalive": "60",
        "cleansession": true,
        "autoUnsubscribe": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closeQos": "0",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willPayload": "",
        "willMsg": {},
        "userProps": "",
        "sessionExpiry": ""
    },
    {
        "id": "f0f882f3.13a8c",
        "type": "server",
        "name": "Home Assistant",
        "version": 5,
        "addon": true,
        "rejectUnauthorizedCerts": true,
        "ha_boolean": "y|yes|true|on|home|open",
        "connectionDelay": true,
        "cacheJson": true,
        "heartbeat": false,
        "heartbeatInterval": 30,
        "areaSelector": "friendlyName",
        "deviceSelector": "friendlyName",
        "entitySelector": "friendlyName",
        "statusSeparator": "at: ",
        "statusYear": "hidden",
        "statusMonth": "short",
        "statusDay": "numeric",
        "statusHourCycle": "h23",
        "statusTimeFormat": "h:m",
        "enableGlobalContextStore": true
    }
]
```
