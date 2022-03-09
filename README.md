# Alexa
Code that creates a AI type function using packets in python
import speech_recognition as sr
import pyttsx3
import datetime
import wikipedia
import pyjokes
import pywhatkit


listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)

def talk(text):
   engine.say(text)
   engine.runAndWait()
def take_command():
    try:
         with sr.Microphone() as source:
              print('listening...')
              voice = listener.listen(source)
              command = listener.recognize_google(voice)
              command = command.lower()
         if 'miku' in command:
              command = command.replace('miku', '')
              print(command)
    except:
        pass
    return command
def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
         song = command.replace('play', '')
         talk('playing' + song)
         pywhatkit.playonyt(song)
    elif 'time' in command:
         time = datetime.datetime.now().strftime('%H:%M')
         print(time)
         talk('current time is' + time)
    elif 'Who is' in command:
         person = command.replace('who is', '')
         info = wikipedia.summary(person, 1)
         print(info)
         talk(info)
    elif 'date' in command:
         talk ('sorry, i have a headache')
    elif 'do you love me' in command:
         talk ('I do love you')
    elif 'joke' in command:
         talk(pyjokes.get_joke())
    else:
         talk('Please say that command again')

while True:
    run_alexa()
