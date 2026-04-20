# Exercise-5
MQTT Reliability, QoS Handshakes, and Retained Messages

--------------------------------------------------------

 Discussion & Architectural Analysis 

Q: If you are designing a battery-powered ESP32 temperature sensor 
that updates every 10 seconds, which QoS level would you choose and why? What are 
the mathematical consequences on battery life and bandwidth if you incorrectly select 
QoS 2 for this scenario? 

A: I'd go with QoS 0 (Fire and Forget). Since we're updating every 10 seconds, losing one packet isn't a big deal-another one is coming right behind it:

Bandwidth: QoS 2 uses 4 packets (the whole handshake) to send one message, while QoS 0 only uses 1. That’s 400% more data for the exact same temperature reading.
Battery Life: The ESP32’s Wi-Fi radio is its biggest "battery vampire."
With QoS 0, it sends the data and sleeps immediately.
With QoS 2, it has to stay awake and keep the radio running while it waits for the broker to reply three different times.
