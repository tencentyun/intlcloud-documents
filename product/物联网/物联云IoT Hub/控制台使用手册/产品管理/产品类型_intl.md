[//]: # (chinagitpath:XXXXX)

There are two types of products that can be created in the IoT Hub Console: general products and NB-IoT products.  
They differ in whether their communication methods and communication modules support secondary development. 
![](https://main.qcloudimg.com/raw/f6e66177d91dad72cd423cdd714e0197/LoRa_product.png)
### General Products 
They use wireless communication (2G/3G/4G/Wi-Fi) or wired communication, and you can perform secondary development on their communication modules to create socket communication.
### NB-IoT Products
They use NB-IoT wireless communication, and you can use the ISP's communication module for communication through the serial port AT commands.
### Gateway Products
They use wireless communication (2G/3G/4G/Wi-Fi) or wired communication. Besides the basic features of general products, they can bind with products that cannot directly connect to the internet such as LoRa products and send messages on their behalf.
### LoRa Products
They use LoRa wireless communication and cannot directly connect to the internet. You need to bind them with gateway products which can send messages on their behalf.





