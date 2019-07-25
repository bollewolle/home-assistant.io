---
layout: page
title: "De Lijn"
description: "Instructions on how to integrate De Lijn (Flemish public transport company) departure times into Home Assistant."
date: 2019-05-23 22:00
sidebar: true
comments: false
sharing: true
footer: true
ha_release: "0.97"
ha_category: 
  - Transport
ha_iot_class: Cloud Polling
ha_qa_scale: 
---

The `delijn` sensor will give you the departure time of the next bus, tram or subway at a specific stop of the De Lijn public transport network in Flanders (Belgium).

## {% linkable_title Setup %}

Create a developer account at [De Lijn Open Data portal](https://data.delijn.be/) to get a free API subscription key.
For valid stop IDs check for the 6 digits at the physical stops or visit the [stops page](https://www.delijn.be/en/haltes/) of the De Lijn website.

## {% linkable_title Configuration %}

To enable this sensor, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: delijn
    api_key: 'API_SUBSCRIPTION_KEY'
    next_departure:
    - stop_id: 'STOP_ID'
      number_of_departures: SET_MAX_NUMBER_OF_PASSAGES
```

{% configuration %}
next_departure:
  description: One or multiple departure sensors.
  required: true
  type: list
  keys:
     subscriptionkey:
      description: "Subscription key needed to access De Lijn API's."
      required: true
      type: string
    stops:
      description: "ID of the stop, e.g. `200552`."
      required: true
      type: string
    number_of_departures:
      description: "Specify the maximal number of passages/departures at a stop to retrieve"
      required: false
      default: 5
      type: integer
{% endconfiguration %}

## {% linkable_title Examples %}

### {% linkable_title Full configuration %}

The example below shows a full configuration with two sensors, only the abcdefg needs to be replaced with an actual API subscription key.

```yaml
# Example configuration.yaml entry
sensor:
  # De Lijn public transport
  - platform: delijn
    api_key: 'abcdefg'
    next_departure:
    - stop_id: '200018'
      number_of_departures: 5
    - stop_id: '201169'
      number_of_departures: 20
```
