![alt tag](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/imgonline-com-ua-twotoone-XpoMD4Mf6S.jpg)

**In this tutorial, we will measure different temperature and humidity data using Temp and humidity sensor. You will also learn how to send this data to AWS.**


# **Hardware** :
- **[ESP-32](https://store.ncd.io/product/esp32-iot-wifi-ble-module-with-integrated-usb/)**:The ESP32 makes it easy to use the Arduino IDE and the Arduino Wire Language for IoT applications. This ESp32 IoT Module combines Wi-Fi, Bluetooth, and Bluetooth BLE for a variety of diverse applications. This module comes fully-equipped with 2 CPU cores that can be controlled and powered individually, and with an adjustable clock frequency of 80 MHz to 240 MHz. This ESP32 IoT WiFi BLE Module with Integrated USB is designed to fit in all ncd.io IoT products.Monitor sensors and control relays, FETs, PWM controllers, solenoids, valves, motors and much more from anywhere in the world using a web page or a dedicated server.We manufactured our own version of the ESP32 to fit into NCD IoT devices, offering more expansion options than any other device in the world! Integrated USB port allows easy programming of the ESP32. The ESP32 IoT WiFi BLE Module is an incredible platform for IoT application development. This ESP32 IoT WiFi BLE Module can be programmed using Arduino IDE.

- **[IoT Long Range Wireless  Temperature And Humidity  Sensor](https://store.ncd.io/product/industrial-long-range-wireless-temperature-humidity-sensor/)**:Industrial Long Range Wireless Temperature Humidity Sensor. Grade with a Sensor Resolution of ±1.7%RH ±0.5°C .Up to 500,000 Transmissions from 2 AA Batteries.Measures -40°C to 125°C with Batteries that Survive these Ratings.Superior 2-Mile LOS Range & 28 miles with High-Gain Antennas.Interface to Raspberry Pi, Microsoft Azure, Arduino and More

- **[Long Range Wireless Mesh Modem with USB Interface](https://store.ncd.io/product/900hp-s3b-long-range-wireless-mesh-modem-with-usb-interface/)**

# **Software Used:**
- Arduino IDE
- AWS

# **Library Used:**
- PubSubClient Library
- Wire.h
- AWS_IOT.h

# Uploading the code  to ESP32 using Arduino IDE:

- **Download and include the PubSubClient Library and Wire.h Library.**
- **Download the Zip file of AWS_IoT ,from the given [link](https://github.com/ExploreEmbedded/Hornbill-Examples) and after extracting ,paste the library in your arduino library folder.**
- **You can get the Arduino code [here](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/AWSIoTEsp32.ino)**
- **You must assign your unique AWS  MQTT_TOPIC,AWS_HOST,SSID (WiFi Name) and Password of the available network.**
- **MQTT topic and AWS HOST can be get inside Things-Interact at AWS-IoT console.**
![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode.JPG)

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode1.JPG)

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode2.JPG)

- **Before uploading the code add certificate inside AWS_IOT folder to aws_iot_certficates.c,which is done in further steps.**
- **Compile and upload the  [ESP32_AWS.ino](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/AWSIoTEsp32.ino) code.**
- **To verify the connectivity of the device and the data sent, open the serial monitor.If no response is seen, try unplugging your ESP32 and then plugging it again. Make sure the baud rate of the Serial monitor is set to the same one specified in your code 115200.**

# Serial monitor output.
![alt tag](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/serial%20monitor%20output.JPG)

# Making the AWS work.

**CREATE THING AND CERTIFICATE**


[![ ALT TEXT](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/vedio1.JPG)](https://www.youtube.com/watch?v=VCReegtku7c)

- THING: It is virtual representation od your device.
- CERTIFICATE: Authenticates the identity of a THING.
- Open [AWS-IoT](https://eu-central-1.console.aws.amazon.com/iot/home)
- Click on manage -THING -Register THING.
- Click on create create single thing.
- Give the Thing name and type.
- Click on next.
- Now your certificate page will open,Click on Create Certificate.
- Download these Certificates,mainly private key,certificate for this thing and root_ca and keep them in separate folder.
- Inside root_ca certificate click on Amazon root CA1-Copy it-Paste  it to notepad and save it as a root_ca.txt file in your certificate folder.

**Create Policy**

[![ ALT TEXT](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/vedio2.JPG)](https://www.youtube.com/watch?v=xxo9oywm4jA)

It defines which operation a device or user can access.
- Go to AWS-IoT interface ,Click on Secure-Policies.
- Click on Create.
- Fill all the necessary details such as policy name,Click Create.
- Now go back to AWS-IoT interface ,Click on Secure-Certificates and attach the policy created just now to it.

**Add Private key,Certificate and root_CA to code.**

- Open your downloaded certificate in your text editor(Notepad++),mainly private key ,root_CA and certificate of thing and edit them as 
the format of aws_iot_certficates.c inside AWS_IOT folder.
- Now open your AWS_IoT folder in your arduino library -My Document.Go to C:\Users\xyz\Documents\Arduino\libraries\AWS_IOT\src ,click on  aws_iot_certficates.c,open it on editor and paste all the edited certificate  their at required place,save it.
![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode3.JPG)

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode4.JPG)

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode5.jpg)
![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/awscode6.jpg)

# Getting Output-

[![ ALT TEXT](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/vedio3.JPG)](https://www.youtube.com/watch?v=IfoH-t8bcpY)

- Go to test in AWS_IoT console.
- Fill your Mqtt topic to Subscription topic in your test credential.
![alt tag](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/test1.JPG)
![alt tag](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/test2.JPG)
- Now you can view yor temp and humidity data.

# OUTPUT
![alt tag](https://github.com/mjScientech/Monitoring-Temp-and-Humidity-using-AWS-ESP32/blob/master/AWS_Output.JPG)



## Steps to make mail alerts.

**You set up Amazon Simple Notification Service (Amazon SNS) for creating mail alert  to receivers address for different temperature and humidity readings.**

[![ ALT TEXT](https://github.com/ncdcommunity/Temp-and-Humidity-Alert-Using-AWS-ESP32/blob/master/Rule%20Vedio.JPG)](https://www.youtube.com/watch?v=S3EDuV-5_3Q)

- Go to AWS IoT console -Click on Act.

- Don't have any rule -Click on create rule.

- On this page Name the rule i.e AlertTempEsp32 ,also provide the description(Creating mail alert of Temp and Humidity sensors data).

- Now create Rule Query Statement(SQL statement for processing data from source).In this the statement used is
```
SELECT * FROM '$aws/things/Temp_Humidity_esp32/shadow/update'

```
- **$aws/things/Temp_Humidity_esp32/shadow/update**,Go to AWS IoT Console -Manage-Thing-Click on your created Thing -Interact.


- To choose an action Click on ADD Action.

- Select send a message as an SNS push notification.

- Now Configure Action selected.for SNS target-choose Create. Enter a name for the SNS topic,such as Temp_Humidity_Esp32Topic.Message Format -**Raw** . Create role -**Temp_Humidity_Esp32TopicRole**.

- Add Action.

- Create rule.

- Create Amazon SNS to send the messages through your Amazon SNS topic to your email inbox.Click on Services .
[![ ALT TEXT](https://github.com/ncdcommunity/Temp-and-Humidity-Alert-Using-AWS-ESP32/blob/master/SNS%20vedio.JPG)](https://www.youtube.com/watch?v=ogmJ8qkFd4c)

- Search SNS.Click on SNS

- In Amazon SNS -Click on Subscription.Select topic ARN.Protocol-Email -Give your email Address on which alert to be send.

- Now click on Create Subscription.

- After clicking the Create Subscription .You have to confirm Subscription by clicking on the mail ,that is send to your registered mail id.

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/Alert20.JPG)

- Confirm Subscrption link
![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/Alert.JPG)

## OUTPUT

![alt tag](https://github.com/mjScientech/Temp-and-Humidity-Alert--AWS-ESP32/blob/master/emailOutput.JPG)
