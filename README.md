**TP2:**

**Analyse de Mosquitto MQTT: Wireshak, autentification et securité**

1. MQTT Analyse (Wireshark)

MQTT protocol is based on top of TCP/IP and both the client and broker need to have a TCP/IP stack.

Below is the snapshot of a subscribe followed by a publish to the same MQTT broker using Wireshark tool from the Catchpoint MQTT monitor. We will be considering a message with the delivery level of QoS t0 here. Let’s dive into a packet-by-packet analysis of the protocol.

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.001.png?raw=true)

1. With wireshark, capture the MQTT communication packets and to display the [**flow graph**] **for publish message**, explain the messages exchanged between the client and the broker.

| <p>![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.002.jpeg)</p><p>![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.003.jpeg)</p><p>[**flow graph**]</p> | ![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.004.png?raw=true) |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------- |

1. Do the same thing with **MQTT subscribe** and display the exchanged messages.
1. Display and describe the content of MQTT message formats :

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.005.png?raw=true)

Use this link to be helped:

<http://blog.catchpoint.com/2017/07/06/dissecting-mqtt-using-wireshark/>

2. MQTT username password

Please follow the following steps to know how to add username and password to mosquitto or MQTT broker.

1)In order to add username and password to the MQTT broker, you need a MQTT broker. If you don’t know how to install MQTT broker please click on the below link.

[**Steps to Install MQTT Broker on Raspberry Pi**](https://bytesofgigabytes.com/mqtt/installing-mqtt-broker-on-raspberry-pi/)

[**Steps to install MQTT Broker on Linux**](https://bytesofgigabytes.com/mqtt/installing-mqtt-broker-on-linux/)

[**Steps to Install MQTT Broker on Google Cloud**](https://bytesofgigabytes.com/googlecloud/installing-mqtt-broker-on-google-cloud/)

2)Assuming you have installed MQTT broker.

3)Now please open the Raspberry pi terminal or Linux system terminal or Google Cloud SSH Terminal

4)Please execute the following command to navigate in the mosquitto installed path

cd /etc/mosquitto

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.006.png?raw=true)
5)Now please execute the following command to create username and password file which is shown below.

sudo mosquitto_passwd -c /etc/mosquitto/pass test

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.007.png?raw=true)
6)Now please enter the password. you can enter anything as your password which is shown below.
![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.008.png?raw=true)

7)Now please execute the following command to check the created username and password file which is shown below

ls

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.009.png?raw=true)

8)Now please execute the following command to modify mosquitto.conf file

sudo nano mosquitto.conf

9)Now please add following lines in mosquitto.conf file which is shown below.

allow_anonymous false
password_file /etc/mosquitto/pass

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.010.png?raw=true)
10)Now we need to restart mosquitto. Now please execute the following command to stop the mosquitto which is shown below.

sudo service mosquitto stop

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.011.png?raw=true)
11)Now please execute the following command to start the mosquitto which is shown below.

sudo service mosquitto start

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.012.png?raw=true)
12)Now please execute the following command to publish data from the terminal using username and password which is shown below.

mosquitto_pub -t test -u test -P test -m hi

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.013.png?raw=true)
13)Now please execute the following command to publish data from the terminal using the wrong username and password and you will get the connection was refused error because username and password are wrong which is shown below.

mosquitto_pub -t test -u test -P tet -m hi

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.014.png?raw=true)
Please click on the below link to become master in MQTT.

2. # Mosquitto SSL Configuration -MQTT TLS Security
   We will configure the mosquitto MQTT broker to use **TLS security**. We will be using openssl to create our own Certificate authority (CA), Server keys and certificates.

will create an **encrypted connection** between the MQTT broker and the MQTT client just like the one between a web browser client and a Web Server.

**At the end verify with Wirshak the encryption of the MQTT message content .**

**Use the tutorial : [http://www.steves-internet-guide.com/mosquitto-tls/**](http://www.steves-internet-guide.com/mosquitto-tls/)\*\*

**Also : [https://youtu.be/f3f4h7q6x5g**](https://youtu.be/f3f4h7q6x5g)\*\*

### **Overview of Steps**

1. Create a **CA** **key pair**
1. Create **CA** **certificate** and use the **CA key** from step 1 to sign it.
1. Create a **broker key pair** don’t password protect.
1. Create a **broker certificate** request using key from step 3
1. Use the **CA certificate** to sign the **broker certificate** request from step 4.
1. Now we should have a **CA key file**,a **CA certificate file**, a **broker key** **file**, and a broker **certificate** **file**.
1. Place all files in a directory on the broker e.g. certs
1. Copy the **CA certificate file** to the client.
1. Edit the **Mosquitto conf** file to use the files -details below
1. Edit the client script to use TLS and the CA certificate.

![create-ca-key](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.015.jpeg)

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.016.png?raw=true)![create-ca-certificate](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.017.jpeg)

![create-server-key](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.018.jpeg)

![create-server-certificate-request](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.019.jpeg)

![create-signed-server-certificate](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.020.jpeg)

![mosquitto-conf-tls](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.021.jpeg)

![](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.022.png?raw=true)![tls-test-script](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.023.jpeg)

![ca-common-name-error](https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images/Aspose.Words.c14b6788-9728-4dff-aae2-6e40713df1b2.024.jpeg)

2

[**flow graph**]: https://www.google.com/url?sa=i&url=https%3A%2F%2Fsubscription.packtpub.com%2Fbook%2Fnetworking_and_servers%2F9781786461674%2F5%2Fch05lvl1sec43%2Fconfiguring-a-flow-graph-for-viewing-tcp-flows&psig=AOvVaw37SIXbBvUFaGoTdggkYk-_&ust=1615616710055000&source=https://github.com/Malek-Zaag/TP1-IOT/blob/main/Images&cd=vfe&ved=2ahUKEwiH7ISyj6rvAhUT_hoKHYeMCF0Qr4kDegUIARClAQ "Configuring a flow graph for viewing TCP flows - Network Analysis using  Wireshark 2 Cookbook - Second Edition"
