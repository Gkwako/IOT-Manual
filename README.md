<img src="https://user-images.githubusercontent.com/90243530/198007126-9f6587bd-6c7d-40d5-92d4-307ca15fa6bc.png" width="auto" height="auto"/>

# How to send and receive data from a Servo motor to Adafruit?
By using this manual, you can send and receive data by connecting to the Internet. The main purpose of the manual is to help beginner or injured gym people by their work-outs and to prevent them from getting more injuries. By making this connection, your physio can track your movement and also see where things go wrong. At the end of the month, you will receive an evaluation of what you can do better.

#
#
# Required hardware components
We need the following hardware:
- 1x NodeMCU basado en ESP8266MOD WiFi incorporado
- 3x Jumper Wires
- 1x RGB LEDstrip Adafruit
<img src="https://user-images.githubusercontent.com/90243530/194128475-d70fe52e-7043-434e-84ad-316df1349f98.png" width="300" height="200"/>

#
#
## Step 1: Install the Arduino IO libraries
In order to establish communication with Adafruit IO, we need to install some additional libraries using the Arduino. First we connect the deck to the computer, and then we open Arduino. Once in Arduino we go straight to library and there we download Adafruit IO Arduino.

<img src="https://user-images.githubusercontent.com/90243530/198085742-80d18763-86a9-4aca-9498-76f32032d51a.png" width="500" height="300"/>

For the Arduino Board quickstart setup, go to https://docs.google.com/document/d/1VLVhwIiPBkJHAkmd1BA77yfsYW7vlDimgMjPT_4U68I/edit and follow the instructions.

#
#
## Step 2: Adafruit IO Account & Feed
To ensure that the physio can read the state ethics on Adafruit IO, an account and feed must first be created. For the account, we go to the following website: https://io.adafruit.com/. See the images 2-4 below for how to make a feed.

<img src="https://user-images.githubusercontent.com/90243530/198086493-cd9c6bf7-281e-44f7-924b-195c8aa8b819.png" width="700" height="400"/>

#
#
## Step 3: Find the yellow key
After creating an account and feed, you need to find the yellow key. The following website: https://learn.adafruit.com/adafruit-io-basics-digital-input?view=all describes how to find the yellow key. When the key appears, you click on the key, and you will get your own IO key that you can use in Arduino to connect to the website.

<img src="https://user-images.githubusercontent.com/90243530/198086905-3763072e-14b8-434e-a033-7ae4a9e488b4.png" width="300" height="400"/>

#
#
## Step 4: Let's start
To connect, we must first enter the Wi-Fi network and the IO key data.

<img src="https://user-images.githubusercontent.com/90243530/198087425-36932f60-8de3-41fe-92eb-5d15b9bf5361.png" width="auto" height="auto"/>

But we now see that there are dots in the serial monitor, this means that there are internet problems, to fix this, I have to use other wifi data.

<img src="https://user-images.githubusercontent.com/90243530/198087592-82a74a4f-b4a4-4c6d-b766-81838b797650.png" width="auto" height="auto"/>

#
#
## Step 5: Send data
We see when we upload, that the data does not go to the new feed name, but to "Connected". It creates a new feed name, to change it you must also give it the correct name in Arduino.

<img src="https://user-images.githubusercontent.com/90243530/198087824-2597e9ac-8d69-4b75-ab74-e3f68bbe537f.png" width="auto" height="auto"/>

Now let's try it out! You see that Gloria following the work-out very well but at some point you see that this has immediately dropped, this is probably due to a small pause. This feed is what the physio sees, you see the calories that have been burned and how long has been trained.

<img src="https://user-images.githubusercontent.com/90243530/198088069-502f9bcd-7089-4655-b6ca-11517740809f.png" width="700" height="400"/>

#
#
## Step 6: The app
Not only can the physio see the progress but also the user via the app. By going to my progress you can see the dashboard with the different measurements

<img src="https://user-images.githubusercontent.com/90243530/198088518-8e4194e9-96e2-488b-bcac-179f20f0a83e.png" width="700" height="400"/>

#
#
## Step 7: Summary send data
When the user performs the workout in front of the mirror. The mirror scans the movements and saves this data on the feed, this feed is saved every time the user makes a movement. In this manual I used the Arduino deck and a button as an example. The Arduino deck represents the mirror and the button is the scan that the mirror performs.

#
#
## Step 8*: How does the silhouette of the mirror work
We know that the mirror helps the user by indicating with a silhout when they are doing something wrong. I will briefly show how we can create this by using LED light and a bot. To install everything, go to https://github.com/Gkwako/IOT-Manuals#ToDo-Telegram.

