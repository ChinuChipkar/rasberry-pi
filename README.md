# rasberry-pi
ultrasonic sensor which plays music
import RPi.GPIO as GPIO
import time
import pygame

# Setup GPIO
GPIO.setmode(GPIO.BCM)
TRIG = 23
ECHO = 24

GPIO.setup(TRIG, GPIO.OUT)
GPIO.setup(ECHO, GPIO.IN)

# Initialize pygame mixer
pygame.mixer.init()
pygame.mixer.music.load("song.mp3")  # Make sure the file is in the same folder

def distance():
    GPIO.output(TRIG, False)
    time.sleep(0.1)

    GPIO.output(TRIG, True)
    time.sleep(0.00001)
    GPIO.output(TRIG, False)

    while GPIO.input(ECHO) == 0:
        pulse_start = time.time()

    while GPIO.input(ECHO) == 1:
        pulse_end = time.time()

    pulse_duration = pulse_end - pulse_start
    dist = pulse_duration * 17150
    return round(dist, 2)

try:
    while True:
        dist = distance()
        print("Distance:", dist, "cm")
        if dist < 30:  # You can adjust the threshold
            if not pygame.mixer.music.get_busy():
                pygame.mixer.music.play()
        time.sleep(1)

except KeyboardInterrupt:
    print("Stopped by user")

finally:
    GPIO.cleanup()
import RPi.GPIO as GPIO
import time
import pygame

# Setup GPIO
GPIO.setmode(GPIO.BCM)
TRIG = 23
ECHO = 24

GPIO.setup(TRIG, GPIO.OUT)
GPIO.setup(ECHO, GPIO.IN)

# Initialize pygame mixer
pygame.mixer.init()
pygame.mixer.music.load("song.mp3")  # Make sure the file is in the same folder

def distance():
    GPIO.output(TRIG, False)
    time.sleep(0.1)

    GPIO.output(TRIG, True)
    time.sleep(0.00001)
    GPIO.output(TRIG, False)

    while GPIO.input(ECHO) == 0:
        pulse_start = time.time()

    while GPIO.input(ECHO) == 1:
        pulse_end = time.time()

    pulse_duration = pulse_end - pulse_start
    dist = pulse_duration * 17150
    return round(dist, 2)

try:
    while True:
        dist = distance()
        print("Distance:", dist, "cm")
        if dist < 30:  # You can adjust the threshold
            if not pygame.mixer.music.get_busy():
                pygame.mixer.music.play()
        time.sleep(1)

except KeyboardInterrupt:
    print("Stopped by user")

finally:
    GPIO.cleanup()
