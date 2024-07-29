# [Note] This branch has some modifications to make it work on the Generic board, ESP32-S3-Devkit-C and INMP441 mems microphone.
  
## Quick Start with ESP-Skainet for Generic ESP32-S3 DevKit-C 

### Pre-requisite

Now this project runs on IDF version 5.x. So install The esp-idf version 5.x

### ESP-Skainet

Make sure you have cloned my project branch with the '--branch'.
Also, need to get all submodules so don't forget the option '--recursive'.

```
git clone --branch ESP32-S3-Devkit-C --recursive https://github.com/Bariest/speech_recognition.git
```

### Example that can be operated in ESP32-DevKit-C and INMP441 

1. Set your I2s microphone settings 

```
cd esp-skainet/components/hardware_driver/boards/include
```

Open the file, 'esp32_s3_devkit_c.h'
```
#define FUNC_I2S_EN         (1)
#define GPIO_I2S_LRCK       (GPIO_NUM_11) (WS)
#define GPIO_I2S_MCLK       (GPIO_NUM_NC) 
#define GPIO_I2S_SCLK       (GPIO_NUM_12) (SCK)
#define GPIO_I2S_SDIN       (GPIO_NUM_10) (SD)
#define GPIO_I2S_DOUT       (GPIO_NUM_NC)
``` 

Modify them for your system.


2. Navigate to one example folder 'esp-skainet/examples/en_speech_commands_recognition'.
```
cd ../../../../examples/en_speech_commands_recognition/
```

3. Set Target and Choose your hardware board
```
idf.py set-target esp32s3
idf.py menuconfig
```
Audio hardware board
-> ESP32-S3-DEVKIT-C

4. Build and flash the project.
```
idf.py build
idf.py flash monitor or idf.py -p com.... flash monitor(com from device manager check port)
```
(if you want to exit the monitor press "ctrl + ]")

5. Advanced users can add or modify speech commands by using the `idf.py menuconfig` command. 
```
idf.py menuconfig
```
Customize the sound from ESP Speech Recognition to customize the wake word

6. To custom or add a new word go back to C:\Espressif\frameworks\esp-idf-v5.2.2\esp-skainet\components\esp-sr\tool
```
pip install g2p_en
python -m pip install numpy 
python -m pip install pandas
python multinet_g2p.py -t "...." (... = English words that you want to add)
```
![image](https://github.com/user-attachments/assets/846da345-53b4-4f82-8bd9-3a6cc4191145)
copy the output for example on this attachment is hcLb WkD
7. go to C:\Espressif\frameworks\esp-idf-v5.2.2\esp-skainet\examples\en_speech_commands_recognition>
```
idf.py fullclean
code .
```
Inside the code 
Right-click sdkconfig --> the click SDK configuration editor
go to add English speech paste in new ID such as INSIDE ID 36..... then save
go to main.c
![image](https://github.com/user-attachments/assets/fec3f6f2-e560-4774-a758-f7bff96bb951)
add case 36
save 
try to run again
```
idf.py clean
idf.py build
idf.py flash monitor or idf.py -p com.... flash monitor(com from device manager check port)

```
Try to speak


