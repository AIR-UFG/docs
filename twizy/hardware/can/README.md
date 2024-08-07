# BUSMASTER Tutorial  
  
## How to set up CAN monitoring  
  
## Summary  
- [Prerequisites](#Prerequisites)  
- [Extra links](#Extra-links)  
- [Tutorial](#Tutorial)  
        - [Enabling PEAK drivers](#Enabling-PEAK-drivers)  
        - [Setting up the CAN Database](#Setting-up-the-CAN-Database)  
- [Recording and playing back CAN data](#Recording-and-playing-back-CAN-data)  
        - [Recording](#Recording)  
        - [Replay](#Replay)  
### Prerequisites  
- [BUSMASTER](https://rbei-etas.github.io/busmaster/) (CAN monitoring software)  
- [tdm-gcc](https://jmeubank.github.io/tdm-gcc/download/) (Required by BUSMASTER)  
- [PEAK driver](https://www.peak-system.com/Drivers.523.0.html?&L=1#) (USB driver)  
- [StreetDrone DBC file](https://github.com/hngu97/StreetDrone-can-interface/blob/master/databases/candatafile.dbc) (StreetDrone CAN database, used for decoding CAN values. Includes GPS/IMU CAN database) (This unofficial repo was found by searching _streetdrone dbc file_, a copy of this file is in this repository but I chose to link the original for archiving purposes)  
### Extra links  
- [PCAN-GPS_Symbols.dbc](https://forum.peak-system.com/viewtopic.php?f=187&t=6382&sid=61755e29ab86053980cbd31992882b61) (GPS/IMU CAN database, used for decoding CAN values)  
- [GPS/IMU manual](https://www.peak-system.com/produktcd/Pdf/English/PCAN-GPS_UserMan_eng.pdf) (Page 39 has information about CAN)  
  
### Tutorial  
After installing all prerequisite programs and the StreetDrone DBC file, open up BUSMASTER. You will be greeted by the following screen:  
![image](https://github.com/user-attachments/assets/452433dd-7159-4eef-bb44-10552f80e442)  
  
#### Enabling PEAK drivers  
Choose the _PEAK USB_ driver from the _Driver Selection_ dropdown menu (located next to the _Connect_ button)  
![image](https://github.com/user-attachments/assets/bf227030-adda-495b-bde4-30e9c14dcb1a)  
  
If connect your computer to the Twizy's CAN usb cable and press _Connect_, you should see this:  
![image](https://github.com/user-attachments/assets/9af73b30-45d8-4324-b8a9-2bdf4da446c6)  
  
We now have access to the CAN data, however, it is still raw. We need the DBC file to decode it into interpretable numbers.  
  
### Setting up the CAN Database  
We will now use our StreetDrone CAN database file (it should be named candatafile.dbc) to map the data frames into values. However, BUSMASTER does not natively understand .dbc files. We need to convert it to .dbf first.  
- Go to the _Tools_ tab and click on _Format Converter_  
![image](https://github.com/user-attachments/assets/91c21264-af9d-4f1d-b080-81dfc0b05eef)  
  
- Go to _Other Converters_  
![image](https://github.com/user-attachments/assets/64348868-2580-4ce8-8a36-24dca12644a3)  
  
- Select _DBC TO DBF Conversion_  
![image](https://github.com/user-attachments/assets/d8c22144-d8bf-485d-86a2-2c8f211a4555)  
  
- Choose the .dbc file (in our case, candatafile.dbc) and click _Convert_  
![image](https://github.com/user-attachments/assets/bffef1a0-0b92-4889-ad14-4fb680325bff)  
  
(you can also choose the output file location but by default it will just put it next to the original with the new file extension)  
  
- Now that we have the correct file format, go back to the _CAN_ tab and click on _Database_ and then _Associate_  
![image](https://github.com/user-attachments/assets/834fc5c4-aadd-4636-a0a6-afd60d94b89d)  
  
- Choose the .dbf file  
  
Your screen should look like this:  
![image](https://github.com/user-attachments/assets/b3209a88-a700-48ff-8102-9b0cfa5d55e4)  
  
  
We now have access to the CAN data, you can double click a Message to see its values.  
![image](https://github.com/user-attachments/assets/fa339c4b-b187-4881-829d-cbbcc7de78af)  
  
  
  
### Recording and playing back CAN data  
Now that we have access to the CAN data, we can record a log of it and play it back whenever we want (like how I'm doing it right now to write this tutorial).  
#### Recording  
- Open the _Logging_ menu and click on _Configure_  
![image](https://github.com/user-attachments/assets/6aab51be-c9f8-4f7d-9a78-e796ba179ef0)  
  
  
- Click on _Add_  
![image](https://github.com/user-attachments/assets/55668978-b2e8-44ea-87da-b78f1e52f470)  
  
This will automatically set a destination file. If you want to choose where the log will be saved, change the _File Path_ by clicking on the _..._ button.  
- After that, click _OK_  
  
The log file is now set, all you have to do is press _Activate_ on the _Logging_ menu  
![image](https://github.com/user-attachments/assets/fd31d51b-1435-484c-96ab-a66e776c12c2)  
  
  
  
#### Replay  
- First, make sure that you are not connected (if you are, press the _Disconnect_ button)  
- Open the _Replay_ menu and click on _Configure_  
![image](https://github.com/user-attachments/assets/0236fe4e-2cf5-4458-8c3b-70cccd7ee937)  
  
- Click on _Add_ and choose the log file recorded on the previous step  
![image](https://github.com/user-attachments/assets/0ff78edb-0a66-425d-99b6-00636e1e5022)  
  
- Click _OK_ and then, when you click on _Connect_ you should see the recording playing back as expected  
- Remember that we still need the .dbf CAN database to interpret the data, so if you are only seeing hexadecimal values in the _Message_ field, be sure to select the .dbf file.
