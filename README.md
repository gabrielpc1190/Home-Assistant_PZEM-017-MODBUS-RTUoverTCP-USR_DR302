# Home-Assistant_PZEM-017-MODBUS-RTUoverTCP-USR_DR302
This is how I connected the PZEM-017 over the network using a RS485 ModBus to TCP adapter with RTUoverTCP

#How to extract data from the PZEM-017 using the USR-DR302 RS485 to TCP with Home Assistant.
+ Make sure you're able to connect your USR-DR302 to your wired network, so your Home Assistant can reach it!
+ All of the registers that worked came from this PDF: https://www.solar-thailand.com/pdf/PZEM-003-Manual.pdf

# modbus integration section on configuration.yaml
```
modbus:
  - name: PZEM_017
    type: rtuovertcp
    host: 172.16.10.98
    port: 8088
    timeout: 5
```

# sensor section on configuration.yaml
```
##########################Modbus Config Test for pzem-017##########################
- platform: modbus
  scan_interval: 10
  registers:
    - name: PZEM_Voltage
      hub: PZEM_017
      unit_of_measurement: V
      slave: 1
      register: 0
      register_type: input
      scale: 0.01
      precision: 2
    - name: PZEM_Current
      hub: PZEM_017
      unit_of_measurement: A
      slave: 1
      register: 1
      register_type: input
      scale: 0.01
      precision: 2
    - name: PZEM_Power_Instant
      hub: PZEM_017
      unit_of_measurement: W
      slave: 1
      register: 2
      register_type: input
      scale: 0.1
      precision: 1
    - name: PZEM_Energy
      hub: PZEM_017
      unit_of_measurement: Wh
      slave: 1
      register: 4
      register_type: input
#    - name: PZEM_High_Voltage_Alarm_Status
#      hub: PZEM_017
#      slave: 1
#      register: 6
#      register_type: input
#    - name: PZEM_Low_Voltage_Alarm_Status
#      hub: PZEM_017
#      slave: 1
#      register: 7
#      register_type: input
```
