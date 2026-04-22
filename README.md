# Speech-to-text-
 Speech-to-Text IIoT (Industrial IoT) project you can build using Python. This example captures voice, converts it to text, and can be extended to send commands to IoT devices.

Requirements
Install these libraries first:
Bash
pip install speechrecognition pyaudio

Basic Speech-to-Text Code
Python
import speech_recognition as sr

# Initialize recognizer
recognizer = sr.Recognizer()

# Use microphone as source
with sr.Microphone() as source:
    print("🎤 Speak something...")
    
    # Adjust for noise
    recognizer.adjust_for_ambient_noise(source)
    
    # Capture audio
    audio = recognizer.listen(source)

try:
    # Convert speech to text using Google API
    text = recognizer.recognize_google(audio)
    print("You said:", text)

except sr.UnknownValueError:
    print("Sorry, could not understand audio")

except sr.RequestError:
    print("API unavailable or error")

IIoT Extension (Control Device Example)
You can connect this with IoT devices like LEDs, motors, etc.
Example: Voice Command → LED Control (Simulation)
Python
if "turn on light" in text.lower():
    print("💡 Light ON command sent to IoT device")

elif "turn off light" in text.lower():
    print("💡 Light OFF command sent to IoT device")

Sending Data to IoT Platform (MQTT Example)
Install MQTT:
Bash
pip install paho-mqtt
Python
import paho.mqtt.client as mqtt

client = mqtt.Client()
client.connect("broker.hivemq.com", 1883, 60)

# Send speech text to IoT server
client.publish("iiot/speech", text)

print("📡 Data sent to IoT platform")