# Virtual-Assistant(Using Python)
   import pyttsx3
import speech_recognition as sr
import webbrowser
import datetime
import wikipedia
import os
import smtplib

# driver code

# create object and assign voice
def speak(audio):
    engine = pyttsx3.init()
    # getter method(gets the current value
    # of engine property)
    voices = engine.getProperty('voices')

    # setter method .[0]=male voice and
    # [1]=female voice in set Property.
    engine.setProperty('voice', voices[1].id)

    # Method for the speaking of the the assistant
    engine.say(audio)

    # Blocks while processing all the currently
    # queued commands
    engine.runAndWait()
# this method is for taking the commands
# and recognizing the command from the
# speech_Recognition module we will use
# the recongizer method for recognizing
def wishMe():
  hour = int(datetime.datetime.now().hour)
  if hour >= 0 and hour < 12:
    speak("Good Morning!")

  elif hour >= 12 and hour < 18:
    speak("Good Afternoon!")

  else:
    speak("Good Evening!")


def takeCommand():
    r = sr.Recognizer()

    # from the speech_Recognition module
    # we will use the Microphone module
    # for listening the command
    with sr.Microphone() as source:
        print('Listening...')

        # seconds of non-speaking audio before
        # a phrase is considered complete
        r.pause_threshold = 0.7
        audio = r.listen(source)

        # Now we will be using the try and catch
        # method so that if sound is recognized
        # it is good else we will have exception
        # handling
        try:
            print("Recognizing...")

            # for Listening the command in indian
            # english we can also use 'hi-In'
            # for hindi recognizing
            Query = r.recognize_google(audio, language='en-in')
            print("the command is printed=", Query)

        except Exception as e:
            print(e)
            speak("Sorry sir Please Say that again")
            return "None"

        return Query


def tellDay():
    # This function is for telling the
    # day of the week
    day = datetime.datetime.today().weekday() + 1

    # this line tells us about the number
    # that will help us in telling the day
    Day_dict = {1: 'Monday', 2: 'Tuesday',
                3: 'Wednesday', 4: 'Thursday',
                5: 'Friday', 6: 'Saturday',
                7: 'Sunday'}

    if day in Day_dict.keys():
        day_of_the_week = Day_dict[day]
        print(day_of_the_week)
        speak("The day is " + day_of_the_week)


def sendEmail(to, content):
  server = smtplib.SMTP('smtp.gmail.com', 587)
  server.ehlo()
  server.starttls()
  server.login('pratichrs526@gmail.com', 'ananya526@')
  server.sendmail('mushakan745@gmail.com', to, content)
  server.close()

def tellTime():
    # This method will give the time
    time = str(datetime.datetime.now())

    # the time will be displayed like
    # this "2020-06-05 17:50:14.582630"
    # nd then after slicing we can get time
    print(time)
    hour = time[11:13]
    min = time[14:16]
    speak( "The time is sir" + hour + "Hours and" + min + "Minutes")


def Hello():
    # This function is for when the assistant
    # is called it will say hello and then
    # take query
    speak("hello sir I am jarvis your desktop assistant. Please tell me how may I assist you ")


def Take_query():
    # calling the Hello function for
    # making it more interactive
    Hello()

    # This loop is infinite as it will take
    # our queries continuously until and unless
    # we do not say bye to exit or terminate
    # the program
    while (True):

        # taking the query and making it into
        # lower case so that most of the times
        # query matches and we get the perfect
        # output
        query = takeCommand().lower()
        if "open amazon" in query:
            speak("Opening Amazon ")

            # in the open method we just to give the link
            # of the website and it automatically open
            # it in your default browser
            webbrowser.open("www.amazon.in")
            continue

        elif "open google" in query:
            speak("Opening Google ")
            webbrowser.open("www.google.com")
            continue
        elif "open whatsapp" in query:
             speak("Openning whatsapp")
             webbrowser.open("https://www.whatsapp.com/?lang=en")
             continue
        elif "open facebook" in query:
             speak("Openning facebook please wait")
             webbrowser.open("www.facebook.com")
             continue
        elif "open youtube" in query:
             speak("Openning youtube")
             webbrowser.open("https://www.youtube.com/")
             continue
        elif "play music" in query:
            speak("oh want to listen music ok wait I am playing it for you")
            webbrowser.open("https://open.spotify.com/album/1qW1C4kDOXnrly22daHbxz?_ga=2.201552725.559383014.1610396951-2070465713.1610396951")
            continue
        elif "play yeh rishta kya kehlata hai" in query:
            speak("ohh ok wait")
            webbrowser.open("https://www.hotstar.com/in/tv/yeh-rishta/586")
            continue
        elif "play bhajans of Durgaa maa" in query:
             speak("ok please wait")
             webbrowser.open("https://www.youtube.com/watch?v=d-EzakpyLyo")
             continue
        elif " Arijit Singh" in query:
            speak("want to listen arijit singh playlist ok wait")
            webbrowser.open("https://in.video.search.yahoo.com/search/video;_ylt=AwrxgKAkrhJgpGIAuSm7HAx.;_ylu=Y29sbwNzZzMEcG9zAzEEdnRpZAMEc2VjA3Nj?p=songs+of+arijit+singh&fr=mcafee#id=1&vid=e0ce5e8fd5ddeb6c07753a38d972a19c&action=view")
            continue
        elif "play songs of Atif Aslam" in query:
            speak("ok please wait just for a minute")
            webbrowser.open("https://open.spotify.com/playlist/0eEm04X62BjvS2Cv2mH3Je")
            continue
        elif "play songs of Neha Kakkar" in query:
            speak("ok wait")
            webbrowser.open("https://open.spotify.com/playlist/4NUJtF3Jx3yUZMq0Kdp0Et")
            continue
        elif "numbers" in query:
            num1 = int(input('Enter First number: '))
            num2 = int(input('Enter Second number: '))
            continue
        elif "addition" in query:
            add = num1 + num2
            print('Sum of ', num1, 'and', num2, 'is :', add)
            continue
        elif "subtract" in query:
            dif = num1 - num2
            print('Difference of ', num1, 'and', num2, 'is :', dif)
            continue
        elif "multiply" in query:
            mul = num1 * num2
            print('Product of', num1, 'and', num2, 'is :', mul)
            continue
        elif "divide" in query:
            div = num1 / num2
            print('Division of ', num1, 'and', num2, 'is :', div)
            floor_div = num1 // num2
            print('Floor Division of ', num1, 'and', num2, 'is :', floor_div)
            continue
        elif "power" in query:
            power = num1 ** num2
            print('Exponent of ', num1, 'and', num2, 'is :', power)
        elif " remainder" in query:
            modulus = num1 % num2
            print('Modulus of ', num1, 'and', num2, 'is :', modulus)
            continue
        elif "day" in query:
            tellDay()
            continue
        elif "which is greater" in query:
            if (num1==num2):
                print("both are equal")
            elif (num1 > num2):
                print(num1)

            else:
                print(num2)

        elif "time" in query:
            tellTime()
            continue

        # this will exit and terminate the program
        elif "bye" in query:
            speak("Bye. Thanks for using me.")
            exit()

        elif "from wikipedia" in query:

            # if any one wants to have a information
            # from wikipedia
            speak("Checking the wikipedia ")
            query = query.replace("wikipedia", "")

            # it will give the summary of 4 lines from
            # wikipedia we can increase and decrease
            # it also.
            result = wikipedia.summary(query, sentences=4)
            speak("According to wikipedia")
            speak(result)
        elif "your name" in query:
            speak("I am Jarvis. Your desktop Assistant")
        elif "who are you" in query:
            speak("I am Jarvis. Your desktop Assistant")
        elif "how are you" in query:
            speak(" I am Fine. what about you")
        elif "what are you doing" in query:
            speak("I am answering your questions answers.")
        elif 'open code' in query:
          codePath = "C:\\Users\\DELL\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
          os.startfile(codePath)

        elif 'email to muskan' in query:
            try:
                speak("What should I say?")
                content = takeCommand()
                to = "mushakan745@gmail.com"
                sendEmail(to, content)
                speak("Email has been sent!")
            except Exception as e:
                print(e)
                speak("Sorry my friend. I am not able to send this email")

if __name__ == '__main__':
    # main method for executing
    wishMe()
    # the functions
    Take_query()
