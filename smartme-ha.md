# Smart Me Integration in Home Assistant


## Yaml
### Sensors
```
modbus:
  - name: smartme_modbus
    host: xxx.xxx.xxx.xxx
    port: 502
    type: tcp
    sensors:
      - name: Kamstrup kWh
        unit_of_measurement: kWh
        address: 8267
        slave: 1
        device_class: energy
        scale: 0.001
        precision: 2
        count: 2
        data_type: int32

      - name: Kamstrup export kWh
        unit_of_measurement: kWh
        address: 8269
        slave: 1
        device_class: energy
        scale: 0.001
        precision: 2
        count: 2
        data_type: int32

      - name: Kamstrup Total Watt
        unit_of_measurement: W
        address: 8195
        slave: 1
        device_class: power
        count: 2
        data_type: int32

      - name: Kamstrup Voltage P1
        unit_of_measurement: V
        address: 8211
        slave: 1
        device_class: voltage
        precision: 0
        scale: 0.001
        count: 2
        data_type: int32

      - name: Kamstrup Voltage P2
        unit_of_measurement: V
        address: 8213
        slave: 1
        device_class: voltage
        precision: 0
        scale: 0.001
        count: 2
        data_type: int32

      - name: Kamstrup Voltage P3
        unit_of_measurement: V
        address: 8215
        slave: 1
        device_class: voltage
        precision: 0
        scale: 0.001
        count: 2
        data_type: int32

      - name: Kamstrup Ampere P1
        unit_of_measurement: A
        address: 8217
        slave: 1
        device_class: current
        precision: 2
        scale: 0.01
        count: 2
        data_type: int32

      - name: Kamstrup Ampere P2
        unit_of_measurement: A
        address: 8219
        slave: 1
        device_class: current
        precision: 2
        scale: 0.01
        count: 2
        data_type: int32

      - name: Kamstrup Ampere P3
        unit_of_measurement: A
        address: 8221
        slave: 1
        device_class: current
        precision: 2
        scale: 0.01
        count: 2
        data_type: int32
```

### Templates
```
- sensor:
    - name: "kamstrup aktuelt forbrug stat"
      unit_of_measurement: W
      state: "{{ states('sensor.kamstrup_total_watt') }}"
      attributes:
        device_class: power
        state_class: measurement
        #last_reset: "{{ state_attr('sensor.eloverblik_energy_total', 'metering_date') }}"
- sensor:
    - name: "kamstrup totalt forbrug stat" #the one that i use on the energy tab
      availability: "{{ states('sensor.kamstrup_kwh') | float > 0 }}"
      unit_of_measurement: kWh
      state: "{{ states('sensor.kamstrup_kwh') }}"
      attributes:
        device_class: energy
        state_class: total_increasing
- sensor:
    - name: "kamstrup totalt export stat" #the one that i use on the energy tab
      availability: "{{ states('sensor.kamstrup_export_kwh') | float > 0 }}"
      unit_of_measurement: kWh
      state: "{{ states('sensor.kamstrup_export_kwh') }}"
      attributes:
        device_class: energy
        state_class: total_increasing

```
