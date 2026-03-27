
import RPi.GPIO as GPIO
import time

# ----------------
# PIN SETUP
# ----------------
PWM_PIN = 18  # ENA (PWM)
DIR_PIN1 = 17  # IN1
DIR_PIN2 = 27  # IN2

GPIO.setmode(GPIO.BCM)
GPIO.setup(PWM_PIN, GPIO.OUT)
GPIO.setup(DIR_PIN1, GPIO.OUT)
GPIO.setup(DIR_PIN2, GPIO.OUT)

# Create PWM @ 1000 Hz
pwm = GPIO.PWM(PWM_PIN, 1000)
pwm.start(0)

try:
# ---- Rotate Forward ----
print("Motor forward")
GPIO.output(DIR_PIN1, GPIO.HIGH)
GPIO.output(DIR_PIN2, GPIO.LOW)
pwm.ChangeDutyCycle(80)  # 0–100% speed
time.sleep(5)

# ---- Stop ----
print("Stop")
pwm.ChangeDutyCycle(0)
time.sleep(2)

# ---- Rotate Backward ----
print("Motor backward")
GPIO.output(DIR_PIN1, GPIO.LOW)
GPIO.output(DIR_PIN2, GPIO.HIGH)
pwm.ChangeDutyCycle(80)
time.sleep(5)

finally:
pwm.stop()
GPIO.cleanup()


