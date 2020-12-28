# My_Projects
 Practice projects, Hello Everyone i have just started exploring this things !! Hope this gives some insight.
 
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
import datetime

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >=0 and hour<12:
        talk("good Morning")


    elif hour>=12 and hour<18:
        talk("Good Afternoon")
    
    else:
        talk("Good Evening")
    
    talk("I am alexa, how may i help you?")

def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
                print(command)
    except:
        pass
    return command


def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    #elif 'stop' in command:
        
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who the heck is' in command:
        person = command.replace('who the heck is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk('sorry, I have a headache')
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')

    elif 'who created you' in command:
        talk('My creator is Sunny ')

    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('Please say the command again.')



if __name__ == "__main__":
    wishMe()


while True:
    run_alexa()

