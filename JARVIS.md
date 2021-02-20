# AI---J.A.R.V.I.S.



from math import e
import pyttsx3
import speech_recognition as speech
import datetime
import os
from requests import get
import wikipedia
import webbrowser
import pywhatkit as kit
import pyjokes
import random
import smtplib
import pyautogui as pag
import cv2

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
print(voices[0].id)
engine.setProperty('voices',voices[0].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def takecommand():
    r = speech.Recognizer()
    with speech.Microphone() as source:
        print("Listening Sir...")
        r.pause_threshold = 1
        audio = r.listen(source,timeout=100,phrase_time_limit=6)
    try:
        print("Recognizing...")
        query = r.recognize_google(audio,language='en-in')
        print(f"user said = {query}")

    except Exception as e :
             #speak("Say that again please...")
             return "none"
    return query

def wish():
    hour = datetime.datetime.now().hour
    if hour >=0 and hour<=12:
        speak("Good Morning Sir...")
    elif hour>12 and hour<18:
        speak("Good Afternoon Sir...")
    else:
        speak("Good Evening Sir...")
    speak("I am jarvis sir. Please tell me how may i help you")

def Calculator(num1,method,num2):
    if "plus" in method:
        a = (f"{num1} + {num2} = {num1+num2}")
        return a
    elif "minus" in method :
        b = (f"{num1} - {num2} = {num1-num2}")
        return b
    elif "into" in method :
        c = (f"{num1} X {num2} = {num1*num2}")
        return c
    elif "sub" in method :
        d = (f"{num1} / {num2} = {num1/num2}")
        return d

def SpeechToText():
    pass

def DateTime():
    a = datetime.date
    print(a)
# def sendEmail(to,content):
#     server = smtplib.SMTP("smtp.gmail.com",587)
#     server.ehlo()
#     server.starttls()
#     server.login('technoruturaj@gmail.com','ruturaj123ashtekar')
#     server.sendmail('technoruturaj@gmail.com',to,content)
#     server.close()



if __name__ == "__main__":
    wish()
    while 1 :
        query = takecommand().lower()
    ##############--PC APP OPENING AND CLOSEING--##############
        if "open notepad" in query:
            apath = "C:\\Windows\\system32\\notepad.exe"
            os.startfile(apath)
        elif "close notepad" in query :
            print("Closing Notepad sir...")
            os.system("taskkill /f /im notepad.exe")
        
        # elif "open browser" in query:
        #     bpath = "C:\\Program Files\\BraveSoftware\\Brave-Browser\\Application\\brave.exe"   
        #     os.startfile(bpath)
        
        elif "open code" in query:
            cpath = "C:\\Users\\HP\\AppData\\Local\\Programs\\Microsoft VS Code\\code.exe"
            os.startfile(cpath)
        elif "open Java" in query :
            path = "C:\\Program Files\\JetBrains\\IntelliJ IDEA Community Edition 2020.3.2\\bin\\idea64.exe"
            os.startfile(path)
        elif "sublime editor" in query :
            path = "C:\\Program Files\\Sublime Text 3\\sublime_text.exe" 
            os.startfile(path)
        elif "close code" in query :
            os.system("taskkill /f /im code.exe")
        elif " close Java" in query :
            os.system("taskkill /f /im idea64.exe")
        elif "close sublime" in query:
            os.system("taskkill /f /im sublime_text.exe")
                
        elif "open spotify" in query:
            dpath = "C:\\Users\\HP\\AppData\\Roaming\\Spotify\\Spotify.exe"
            os.startfile(dpath)
        elif "close spotify" in query:
            os.system("taskkill /f /im Spotify.exe")
        
        elif "open discord" in query:
            dpath = "C:\\Users\\HP\\AppData\\Local\\Discord\\app-0.0.309\\Discord.exe"
            os.startfile(dpath)
        elif "close discord" in query:
            os.system("taskkill /f /im Discord.exe")
        

        elif "open terminal" in query:
            os.system("start cmd")
        #These are the chat commands
        
        elif "greet" in query:
            runwish = wish()
            a = f"{runwish}"
            b = speak(a)
        elif "awesome jarvis" in query:
            speak("Thank You sir i am always there for you sir...")
        
        elif "hey jarvis" in query:
            speak("Yes sir. Do you want something ?")
        elif "I just forget it" in query :
            speak("Remember it Sir! it will be something important.")
        
        elif "what is a time Jarvis" in query:
            time = datetime.time()
            speak(f"{time}")

#       Tasks To GO...
        elif "switch window" in query:
            speak("Switching Window sir...")
            pag.keyDown("alt")
            pag.press("tab")
            # time.sleep("1")
            pag.keyUp("alt")
        
        elif "open camera" in query:
            cap = cv2.VideoCapture(0)
            while True:
                ret,img = cap.read()
                cv2.imshow("webcam",img)
                k = cv2.waitKey(50)
                if k==27 :
                    break;
            cap.release()
            cv2.destroyAllWindows()

        
        elif "what is my ip" in query:
            ip = get('https://api.ipify.org').text
            speak(f"your ip is {ip} sir")
            print(f"your ip is {ip} sir")
        
        elif "wikipedia" in query:
            speak("Searching Wikipedia...")
            query = query.replace("wikipedia","")
            result = wikipedia.summary(query,sentences=2)
            speak("According To wikipedia...")
            speak(result)
            print(result)
        
        elif "open youtube" in query:
            webbrowser.open("www.youtube.com")
        elif "go to channel" in query:
            pass
        
        
        elif "open google" in query:
            speak ("Sir, What should i search for you")
            cm = takecommand().lower()
            kit.search(f"{cm}")
        elif "close google" in query:
            os.system("taskkill /f /im brave.exe")


        elif "emails" in query:
            speak("What do you want to check sir?")
            query = takecommand().lower()
            if "inbox" in query:
                webbrowser.open("https://mail.google.com/mail/u/2/#inbox")
            elif "send" in query :
                webbrowser.open("https://mail.google.com/mail/u/2/#sent")
        
        elif "play video on youtube" in query:
            speak ("which video do you want to play on youtube sir ?")
            cm = takecommand().lower()
            kit.playonyt(f"{cm}")
       
        elif "joke" in query :
            joke = pyjokes.get_joke()
            speak(joke)
 
        elif "shutdown pc" in query :
            speak("System turning off...")
            os.system("shutdown /s /t 5")    
        elif "restart system" in query:
            speak("Restarting System Sir...")
            os.system("shutdown /r /t 5")
        elif "go to sleep" in query :
            speak("Going to Sleep sir...")
            os.system("rundll32.exe powrprof.dll,SetSuspendState 0,1​,0")
        elif "stop" in query :
            break
