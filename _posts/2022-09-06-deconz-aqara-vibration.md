---
title: Configuring sensitivity of Aqara Vibration Sensor using deCONZ (Home Assistant)
---

I have a vibration sensor from Aqara which monitors my laundry machine.
However, the default sensitivity of the sensor is not sensitive enough to notice when the machine is running.

_Side note, I was extremely surprised when I put my hand on the machine during.
Even during its rinsing cycle, the vibrations barely reach the plastic shell of the machine.
Well done Bosch!_

# Modifying the sensitivity

Since I do not have the Aqara Hub, but instead use Home Assistant with a Conbee USB stick and the deCONZ integration,
I went online to find a way to modify the sensitivity of the sensor.

I found [this excellent post](https://blog.galt.me/home-assistant-deconz-zigbee-rest-api-usage/) which explains
_almost_ everything you need to know.
There are two key things lacking though, and I will present them in this post.

## Find your sensor's number

In the post above, the author writes:

> There is one last piece of information we need to get before we can proceed and that is your entity id.
> This is a two digit number that is assigned to your vibration sensor.
> You can easily find this in Home Assistant by checking Configuration --> Entities and searching for your
> binary_sensor.vibration entity.
>
> This will have a number at the end of the name, in this example mine is called binary_sensor.vibration_28.
> So my entity id is 28.

This is only the case if you do not modify the default entity_id provided by the deCONZ Integration.
I prefer to _always_ modify my entities to give them more descriptive values.
The vibration sensor of interest in this post, for instance, is called
`binary_sensor.laundry_vibration_sensor`.

Luckily, it is possible to ask deCONZ about the required number.

If you omit the number in the API call from the post above, deCONZ will return data for _all_ sensors.

```shell
$> curl -X GET http://172.30.33.2:40850/api/FDDA4762E9/sensors
```

My truncated output (I have omitted everything except the vibration sensor data) looks like this:

```shell
"9": {
        "config": {
            "battery": 100,
            "on": true,
            "pending": [
                "sensitivity"
            ],
            "reachable": true,
            "sensitivity": 1,
            "sensitivitymax": 21,
            "temperature": 1900
        },
        "ep": 1,
        "etag": "c7e0a9016f4bcad6c302323d844f0096",
        "lastannounced": null,
        "lastseen": "2022-09-06T05:33Z",
        "manufacturername": "LUMI",
        "modelid": "lumi.vibration.aq1",
        "name": "Washing machine vibration sensor",
        "state": {
            "lastupdated": "2022-09-06T03:47:35.761",
            "orientation": [
                0,
                0,
                0
            ],
            "tiltangle": 0,
            "vibration": false,
            "vibrationstrength": 2
        },
        "swversion": "20180130",
        "type": "ZHAVibration",
        "uniqueid": "00:15:8d:00:08:52:a2:62-01-0101"
    }
```

The `"9"` at the very beginning of the block is the `<number>` you need!

## Waiting for the sensitivity to change

The keen eyed reader might have noticed that the JSON above has a list named `"pending"` which in turn contains
`"sensitivity"`.

According to
[robertklep in the Home Assistant forum](https://community.home-assistant.io/t/set-the-sensitivity-for-xiaomi-vibration-sensor-through-rest-api-deconz/95543/38?u=erikthorsell),
this is deCONZ informing us that the sensitivity change will take effect next time the sensor wakes up from sleep.
robertklep continues to write that it is possible to short press the button on the sensor every few seconds to make
the sensor adopt the new sensitivity sooner, but I was not successful in doing so.

# Conclusion

Nevertheless, these were the two things I lacked when reading through the blog post.
Hopefully this helps you too!