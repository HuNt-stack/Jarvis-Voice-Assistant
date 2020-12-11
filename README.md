# Jarvis-Voice-Assistant

import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')

print(voices[1].id)
engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour < 12:
        speak("good morning ")
    elif hour >= 12 and hour < 18:
        speak("good afternoon")
    else:
        speak("good evening")


speak("i am jarvis . please tell me how may i help you")


def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("listening.......")
        pause_threshold = 1
        audio = r.listen(source)
    try:
        print("recognizing....")
        query = r.recognize_google(audio, language='en=in')
        print(f"User said: {query}\n")

    except Exception as e:
        print(e)
        print("say that again please.... ")
        return "None"
    return query


if __name__ == "__main__":
    wishMe()
    while True:
        query = takeCommand().lower()
        if 'wikipedia' in query:
            speak('searching wikipedia....')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to wikipedia")
            print(results)
            speak(results)
        elif 'open youtube' in query:
            webbrowser.open("youtube.com")
        elif 'open google' in query:
            webbrowser.open("google.com")
        elif 'open hangouts' in query:
            webbrowser.open("hangouts.com")
        elif 'thank you jarvis' in query:
            speak('your welcome')
        elif 'open stack overflow' in query:
            webbrowser.open("stackoverflow.com")
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M")
            speak(f"sir , the time is{strTime}")
            print(strTime)
        elif 'open chord' in query:
            codePath = "C:\\Users\\amitm\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)
        elif 'open webstorm' in query:
            codePath = "C:\\Program Files\\JetBrains\\WebStorm 2020.2.2\\bin\\webstorm64.exe"
            codePath = "C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe"

        elif 'i am happy ' in query:
            speak("your happiness makes me happy")
        elif 'open google drive' in query:
            webbrowser.open("drive.google.com")
        elif 'okay jarvis' in query:
            speak('as you wish')
            exit()
        elif 'that is enough jarvis' in query:
            speak('as you wish')
            exit()

        elif 'good morning ' in query:
            speak('good morning sir')
        elif 'good afternoon' in query:
            speak('good afternoon sir')
        elif 'good evening' in query:
            speak('good evening')
        elif 'good night' in query:
            speak('good night')
            os.startfile(codePath)
        elif 'open google' in query:

        elif 'bye'  in query:
            speak('Bye')


#this code is written in python . This code will help you to make a voice-assistant . 
