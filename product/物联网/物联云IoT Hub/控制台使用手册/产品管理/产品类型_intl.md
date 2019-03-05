[//]: # (chinagitpath:XXXXX)

There are two types of products that can be created in the IoT Hub Console: standard products and NB-IoT products.  
The difference is whether their communication methods and modules support re-development.
![](https://main.qcloudimg.com/raw/f6e66177d91dad72cd423cdd714e0197/LoRa_product.png)
### Standard Products 
Standard Products use wireless (2G/3G/4G/Wi-Fi) or wired communication, users can re-develop modules and create socket communication.
### NB-IoT Products
NB-IoT Products use NB-IoT wireless communication. Users use the ISP's communication modules and serial port AT for communications.
### Gateway Products
Gateway products use wireless (2G/3G/4G/Wi-Fi) or wired communication. Besides having basic features of general products, they can also bind to products such as LoRa which cannot connect to Internet directly and send messages on their behalf. 
### LoRa Products
LoRa Products use LoRa wireless communication and cannot connect to the internet directly. You need to bind them with gateway products which send messages on their behalf.





