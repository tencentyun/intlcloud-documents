When creating a product in the IoT Hub console, you can select general product or gateway product as the product type. Their differences lie in the communication method and whether the communication module can be further developed.
 
### General Product 
A general product communicates over 2G/3G/4G/Wi-Fi or wired connection. You can further develop its communication module to implement socket communication.


### Gateway Product
A gateway product communicates over 2G/3G/4G/Wi-Fi or wired connection. In addition to the basic features of general products, it can also be bound to products that cannot directly access the internet and send messages on their behalf, such as LoRa products.

### LoRa Product
A LoRa product communicates over LoRa and cannot directly access the internet. It uses the standard LoRaWAN protocol and relies on a gateway to send messages on its behalf.


### CLAA Product
A CLAA product communicates over LoRa and cannot directly access the internet. It uses the CLAA protocol (with a built-in CLAA module) and relies on a gateway to send messages on its behalf.




