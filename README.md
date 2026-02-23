
import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import os

engine = pyttsx3.init()

def speak(text):
    print("Robot:", text)
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)
    try:
        command = r.recognize_google(audio)
        print("You:", command)
        return command.lower()
    except:
        return ""

def run_robot():
    speak("Hello, I am your AI robot")

    while True:
        cmd = listen()

        if "time" in cmd:
            now = datetime.datetime.now().strftime("%H:%M")
            speak(f"The time is {now}")

        # elif "open youtube" in cmd:
        #     webbrowser.open("https://youtube.com")
        #     speak("Opening YouTube")

        # elif "open google" in cmd:
        #     webbrowser.open("https://google.com")
        #     speak("Opening Google")

        elif "open" in cmd:
            site = cmd.replace("open", "").strip()

            if site:
                url = f"https://{site}.com"
                webbrowser.open(url)
                speak(f"Opening {site}")

        elif "stop" in cmd or "exit" in cmd:
            speak("Goodbye")
            break

if __name__ == "__main__":
    run_robot()
