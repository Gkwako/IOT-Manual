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
## Install the Arduino IO libraries
In order to establish communication with Adafruit IO, we need to install some additional libraries using the Arduino. 

First we connect the deck to the computer, and then we open Arduino. 

<img width="516" alt="Schermafbeelding 2022-10-26 om 23 21 17" src="https://user-images.githubusercontent.com/90243530/198140804-fcee4354-3c4f-4955-80e3-b603625b27a6.png"><img width="516" alt="Schermafbeelding 2022-10-26 om 23 21 47" src="https://user-images.githubusercontent.com/90243530/198140823-0b646c9c-2601-41f4-ad1f-8a15b6e3a957.png">

Once in Arduino we go straight to library and there we download Adafruit IO Arduino.

<img src="https://user-images.githubusercontent.com/90243530/198085742-80d18763-86a9-4aca-9498-76f32032d51a.png" width="500" height="300"/>

For the Arduino Board quickstart setup, go to https://docs.google.com/document/d/1VLVhwIiPBkJHAkmd1BA77yfsYW7vlDimgMjPT_4U68I/edit and follow the instructions.

#
#
## Adafruit IO Account & Feed
To ensure that the physio can read the state ethics on Adafruit IO, an account and feed must first be created. For the account, we go to the following website: https://io.adafruit.com/. See the images 2-4 below for how to make a feed.

<img src="https://user-images.githubusercontent.com/90243530/198086493-cd9c6bf7-281e-44f7-924b-195c8aa8b819.png" width="700" height="400"/>

#
#
## Find the yellow key
After creating an account and feed, you need to find the yellow key. The following website: https://learn.adafruit.com/adafruit-io-basics-digital-input?view=all describes how to find the yellow key. When the key appears, you click on the key, and you will get your own IO key that you can use in Arduino to connect to the website.

<img src="https://user-images.githubusercontent.com/90243530/198086905-3763072e-14b8-434e-a033-7ae4a9e488b4.png" width="300" height="400"/>

#
#
## Let's start connecting
To connect, we must first enter the Wi-Fi network and the IO key data.

<img src="https://user-images.githubusercontent.com/90243530/198087425-36932f60-8de3-41fe-92eb-5d15b9bf5361.png" width="auto" height="auto"/>

    #define IO_USERNAME "....."
    #define IO_KEY "...._...."
    
    #define WIFI_SSID "......."                 
    #define WIFI_PASS "........."

But we now see that there are dots in the serial monitor, this means that there are internet problems, to fix this, I have to use other wifi data.

<img src="https://user-images.githubusercontent.com/90243530/198087592-82a74a4f-b4a4-4c6d-b766-81838b797650.png" width="auto" height="auto"/>

By using a different network you can see in the 2nd picture that the connection was successful, causing the Arduino deck to glow a blue light.

#
#
## Send data
We see when we upload, that the data does not go to the new feed name, but to "Connected". It creates a new feed name, to change it you must also give it the correct name in Arduino.

<img src="https://user-images.githubusercontent.com/90243530/198087824-2597e9ac-8d69-4b75-ab74-e3f68bbe537f.png" width="auto" height="auto"/>
        
    AdafruitIO_Feed *digital = io.feed(".......");

Now let's try it out! You see that Gloria following the work-out very well but at some point you see that this has immediately dropped, this is probably due to a small pause.

<img src="https://user-images.githubusercontent.com/90243530/198088069-502f9bcd-7089-4655-b6ca-11517740809f.png" width="700" height="400"/>

This feed is what the physio sees, you see the calories that have been burned and how long has been trained.

#
#
## Giving feedback with Ledlight
Now that we have succeeded in getting data, we want to get this feedback in the form of colors, we will do this through Led light. For this we have to plug the LED light on the Arduino deck. 

Connecting wires (THE WIRES MAY HAVE OTHER COLORS)
-  Wire from 5V to 3V3
- Middle wire (Din) to D5*
- GND wire to GND

<img width="533" alt="Schermafbeelding 2022-10-26 om 23 34 32" src="https://user-images.githubusercontent.com/90243530/198142821-90a67ae3-d218-4920-9a3e-ff3952197ba7.png">

*can you also not read the pins on your NodeMCU? Then look for the pins via the https://duckduckgo.com/?t=ffab&q=nodemcu&iax=images&ia=images

Now paste the code of the Ledlight into the data receiver. 
this is the code: 

    #include "config.h"
    #include <FastLED.h>

    // digital pin 5
        #define BUTTON_PIN D0
        #define NUM_LEDS 9

        #define DATA_PIN D5
        #define CLOCK_PIN 13

        CRGB leds[NUM_LEDS];

    // button state
        bool current = false;
        bool last = false;

    // set up the 'digital' feed
        AdafruitIO_Feed *digital = io.feed("progress");

    void setup() {
    FastLED.addLeds<WS2811, DATA_PIN, RGB>(leds, NUM_LEDS);
   
    // set button pin as an input
        pinMode(BUTTON_PIN, INPUT);

    // start the serial connection
        Serial.begin(115200);

    // wait for serial monitor to open
        while(! Serial);

    // connect to io.adafruit.com
        Serial.print("Connecting to Adafruit IO");
        io.connect();

    // wait for a connection
        while(io.status() < AIO_CONNECTED) {
        Serial.print(".");
        delay(500);
        }

    // we are connected
        Serial.println();
        Serial.println(io.statusText());
        }

        void loop() {
        for(int whiteLed = 0; whiteLed < NUM_LEDS; whiteLed = whiteLed + 1) {
      
      // Turn our current led on to white, then show the leds
        leds[whiteLed] = CRGB::White
        ;

      FastLED.show();

      // Wait a little bit
        delay(700);

      // Turn our current led back to black for the next loop around
        leds[whiteLed] = CRGB::Red
        ;

      // io.run(); is required for all sketches.
      // it should always be present at the top of your loop
      // function. it keeps the client connected to
      // io.adafruit.com, and processes any incoming data.
    
    io.run();

      // grab the current state of the button.
      // we have to flip the logic because we are
      // using a pullup resistor.
          if(digitalRead(BUTTON_PIN) == LOW)
            current = true;
          else
            current = false;

      // return if the value hasn't changed
          if(current == last)
            return;

      // save the current state to the 'digital' feed on adafruit io
          Serial.print("sending button -> ");
          Serial.println(current);
          digital->save(current);

      // store last button state
          last = current;
           }
        }

The led light is on, but it doesn't seem to work when I click the button. But in the Serial Monitor you can see that the data is sending.

    21:13:16.658 -> Adafruit IO connected.
    21:13:21.521 -> sending button -> 1
    21:13:23.164 -> sending button -> 0
    21:13:34.529 -> sending button -> 1
    21:13:35.320 -> sending button -> 0

okey the problem turns out to be with the color settings, if I change the color to white and blue I get the light off and on.

      leds[whiteLed] = CRGB::White;
      FastLED.show();

      // Wait a little bit
            delay(700);

      // Turn our current led back to black for the next loop around
        leds[whiteLed] = CRGB::Blue;

https://user-images.githubusercontent.com/90243530/198120488-6ae0ae74-4f65-417e-8401-fb18949877d4.mov

Let's check the adafruit feed, you should see something like this.

<img src="https://user-images.githubusercontent.com/90243530/198126545-5d4aa8d8-4bdf-4258-83d5-c4f52fdba96a.png" width="700" height="400"/>

In the feed you see activity. By clicking on the button, data is sent to the feed, while this data is being sent you get visual feedback back because the light is flickering.

<img src="https://user-images.githubusercontent.com/90243530/198131524-aa67e661-8dc5-4cd5-8fb8-e7b6c43424ba.PNG" width="200" height="200"/><img src="https://user-images.githubusercontent.com/90243530/198131531-8814150c-b27d-4e3f-afed-3f877e1f18bc.PNG" width="200" height="200"/><img src="https://user-images.githubusercontent.com/90243530/198131524-aa67e661-8dc5-4cd5-8fb8-e7b6c43424ba.PNG" width="200" height="200"/>

#
#
## The app
Not only can the physio see the progress but also the user via the app. By doing the progress you can see the dashboard with the different measurements

<img src="https://user-images.githubusercontent.com/90243530/198088518-8e4194e9-96e2-488b-bcac-179f20f0a83e.png" width="700" height="400"/>
https://www.figma.com/proto/lOkrlrQppnPKSpm86yZTMG/AI---Artificial-Intelligence?page-id=1%3A3&node-id=38%3A285&starting-point-node-id=38%3A279

#
#
## Summary send data
When the user performs the workout in front of the mirror. The mirror scans the movements and saves this data on the feed, this feed is saved every time the user makes a movement. In this manual I used the Arduino deck a button and led lights as an example. The Arduino deck represents the mirror and the button is the scan that the mirror performs, the led light is the feedback that is being sent to the feed.

Now you know how to send feedback and see it visually.

#
#
## Extra: How does the silhouette of the mirror work
We know that the mirror helps the user by indicating with a silhout when they are doing something wrong. I will briefly show how we can create this by using LED light and a bot. To install everything, go to https://github.com/Gkwako/IOT-Manuals#ToDo-Telegram.

