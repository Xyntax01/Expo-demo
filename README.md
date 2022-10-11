# Lees dit!

Lees deze hele lastige documentatie om te weten hoe je de demo werkend kan krijgen

# Stap 1

Clone de repo en installeer Laravel, de compose packages en npm packages

## Stap 2

Installeer de docker containers

    git clone https://github.com/FIWARE/tutorials.IoT-Agent.git
    cd tutorials.IoT-Agent
    ./services create ./services start
als de services create en start niet werken gebruik dan de command

    docker compose up

## Stap 3

Maak de lamp en deurbel aan met dit command in Postman
**Lamp**

    curl -iX POST \ 'http://localhost:4041/iot/devices' \ -H 'Content-Type: application/json' \ -H 'fiware-service: openiot' \ -H 'fiware-servicepath: /' \ -d  '{ "devices": [ { "device_id": "lamp001", "entity_name": "urn:ngsi-ld:Lamp:001", "entity_type": "Lamp", "protocol": "PDI-IoTA-UltraLight", "transport": "HTTP", "endpoint": "http://iot-sensors:3001/iot/lamp001", "commands": [ {"name": "on","type": "command"}, {"name": "off","type": "command"} ], "attributes": [ {"object_id": "s", "name": "state", "type":"Text"}, {"object_id": "l", "name": "luminosity", "type":"Integer"} ], "static_attributes": [ {"name":"refStore", "type": "Relationship","value": "urn:ngsi-ld:Store:001"} ] } ] } '

**Deurbel**

    curl -iX POST \ 'http://localhost:4041/iot/devices' \ -H 'Content-Type: application/json' \ -H 'fiware-service: openiot' \ -H 'fiware-servicepath: /' \ -d  '{ "devices": [ { "device_id": "bell001", "entity_name": "urn:ngsi-ld:Bell:001", "entity_type": "Bell", "protocol": "PDI-IoTA-UltraLight", "transport": "HTTP", "endpoint": "http://iot-sensors:3001/iot/bell001", "commands": [ { "name": "ring", "type": "command" } ], "static_attributes": [ {"name":"refStore", "type": "Relationship","value": "urn:ngsi-ld:Store:001"} ] } ] } '

## Stap 5

Run dit command zodat je de site ook kan gebruiken op een smartphone

    php artisan serve --host 0.0.0.0(local ip) --port=8000

