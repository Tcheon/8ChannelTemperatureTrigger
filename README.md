# 8ChannelTemperatureTrigger
import Adafruit_DHT as dht
import RPi.GPIO as GPIO
from time import sleep

GPIO.setmode(GPIO.BCM)

h,t = dht.read_retry(dht.DHT22, 4)
print ('Temp={0:0.1f}*C  Humidity={1:0.1f}%'.format(t, h))

while True :
    h,t = dht.read_retry(dht.DHT22, 4)
    hum = '{1:0.1f}'.format(t,h)
    print(hum) #for teste mode
    if hum > "60" :#  SET HERE THE TEMPERATURE REQUESTED


        GPIO.setup(17, GPIO.OUT) #  SET HERE WHICH GPIO
        GPIO.output(17, GPIO.LOW) #Turn on
        print("too humid, turning on fans!!")
        sleep(3)
        GPIO.output(17, GPIO.HIGH) #Turn off
        sleep(3)
        GPIO.output(17, GPIO.LOW)



