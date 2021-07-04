import datetime as sr

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getproperty('voices')
engine.setProperty('voice', voices[1].id)


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
            if 'yash' in command:
                command = command.replace('yash','')
                print(command)
    except:
        pass
    return command 
    
    
def run_yash():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play','')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('current time is ' + time)
    elif 'who the heck is' in command:
        person = command.replace('who the heck is' , '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'do you know yashwin kadian' in command:
        talk('yes he is my developer and made me using python language')
    elif 'how justin bieber became singer' in command:
        talk('a singer usher heard him singing on youtube and took justin by his parents consent for singing')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('please say the command again.')
        
        
while True:
    run_yash()
