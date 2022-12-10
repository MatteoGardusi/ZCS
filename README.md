## Usage:
Obtain your Device Serial/ThingKey and your Authorization header value from ZCS Zucchetti.

Add to configuration.yaml:

```
sensor:
  - platform: zcsazzurro
    name: fotovoltaico
    thingkey: [YOUR DEVICE SERIAL - THINGKEY]
    authkey: [YOUR AUTHORIZATION HEADER VALUE]
    clientcode: [YOUR CLIENT CODE HERE]    
    
```

## Example for extract sensor
```
sensor:
  - platform: integration
    name: power_generating_spent_zcs
    source: sensor.power_generating_zcs
    unit_prefix: k
    round: 2    
    method: left
    
##### current   
template:
  - sensor:
      - name: "Potenza Istantanea"
        unit_of_measurement: "W"
        state: >
          {% set power = state_attr('sensor.fotovoltaico','current')['powerGenerating'] | int(0) %}
          {{ power }}
        state_class: measurement
        device_class: power
        icon: mdi:solar-power

      - name: "Batteria"
        unit_of_measurement: "%"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['batterySoC'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:battery-90
        
      - name: "Consumo Giorno Casa"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyConsuming'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:power-socket-it  
        
      - name: "Autoconsum Giorno"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyAutoconsuming'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:power-plug-outline    
        
      - name: "Scarica"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyDischarging'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:battery-low 
        
      - name: "Carica"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyCharging'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:battery-high 
        
      - name: "Produzione"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyGenerating'] | float(0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:solar-power
        
      - name: "Prelievo"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyImporting'] | float(0)%}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:transmission-tower  
        
      - name: "Immissione"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','current')['energyExporting'] | float (0) %}
          {{ energy | round(2) }}
        state_class: measurement
        device_class: energy
        icon: mdi:solar-power 
           
##### total         
      - name: "Produzione Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyGenerating'] | float(0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:weather-sunny
        
      - name: "Prelievo Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyImporting'] | float (0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:transmission-tower
        
      - name: "Immissione Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyExporting'] | float(0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:flash-circle
        
      - name: "Autoconsum Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyAutoconsuming'] | float(0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:power-plug-outline 
        
      - name: "Scarica Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyDischarging'] | float(0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:battery-low
        
      - name: "Carica Totale"
        unit_of_measurement: "kWh"
        state: >
          {% set energy = state_attr('sensor.fotovoltaico','total')['energyCharging'] | float(0) %}
          {{ energy | round(2) }}
        state_class: total_increasing
        device_class: energy
        icon: mdi:battery-high
```

## Example sensor for energy panel
```
utility_meter:
  total_energy_generating_zcs:
    source: sensor.energy_generating_zcs
    cycle: daily

  total_energy_exporting_zcs:
    source: sensor.energy_exporting_zcs
    cycle: daily

  total_energy_importing_zcs:
    source: sensor.energy_importing_zcs
    cycle: daily
```

## Authors & contributors

The original setup of this repository is by [SDeSalve][sdesalve].

Thanks to Alesoft73 for their support to implement new API.

## License

Copyright (c) 2021 SDeSalve

See [LICENSE][license]

## Trademark legal notice

This integration is not created, developed, affiliated, supported, maintained or endorsed by **Zucchetti Centro Sistemi S.p.A.**.
All product names, logos, brands, trademarks and registered trademarks are property of their respective owners. All company, product, and service names used are for identification purposes only.
Use of these names, logos, trademarks, and brands does not imply endorsement.


[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/sdesalve/zcsazzurro)

[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-2.svg
[buymeacoffee]: https://www.buymeacoffee.com/sdesalve
[paypal-shield]: https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif
[paypal]: https://paypal.me/SDeSalve
[license]: https://github.com/sdesalve/zcsazzurro/LICENSE.md
[sdesalve]: https://github.com/sdesalve
