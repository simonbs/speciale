#Plan for User Tests of CARMA
[toc]

This document will outline how and what we plan to test during our user tests.

##Purpose
The purpose of the user tests is to obtain knowledge regarding how well the system performs when used by people who have no prior experience with it. We wish to gain at least an indication of how well the gesture recognizer performs, meaning how many times it correctly identifies the gesture performed by the user.
As well we wish to gain at least an indication of how well the recommender performs, meaning how many times it correctly identifies the intended action of the user.
_This will **not** test technical aspects such as how much RAM is consumed, how much power is used or how computationally expensive it is._

###Gesture Recognizer Goal
We wish to achieve knowledge about how well the gesture recognizer performs. Performance in this context means how often a gesture is correctly recognized.
> A gesture is considered _correctly recognized_ if it is the gesture the user _intended_ to perform

###Recommender System Goal
We wish to achieve knowledge about how well the recommender system performs. Performance in this context means how often the system performs the correct action.
> An action is considered _correct_ if it is the _intended_ action of the user.

##Setup
This section will describe the setup of the tests such as where they will take place, how many people will be involved as well as other details.
###Location
The tests will take place in the Cassiopeia building. Room not yet specified.
Preferably it will take place in two connected rooms so that we may test with more realistic positioning probabilities, but in the event that only one room is available to us, we will simple switch some of the Estimote beacons off to simulate the user leaving a room.
###Date and Time
Date yet to be determined.
###Participants
Participants yet to be determined. Expected to be friends and other students.
###Gear
The gear used for the test will be:
 - [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
 - Android phone (Model yet to be specified)
 - [Moto 360 Smart Watch](https://www.motorola.com/us/products/moto-360)
 - MacBook Pro For logging data
 - MacBook Pro for running Spotify

###Procedure
####Initial / technical setup
As the wireless network available at Cassiopeia is unfit for communication over WLAN we will either set up our own wireless network or utilize NGrok.
The smart watch will have its databases of templates and action configurations cleared prior to each new participant.
####Introduction
The participant is introduced to the project and relevant data regarding the person (such as age and gender perhaps) is noted. The participant will also have the test explained.
####Setup of gestures
The participant is asked to create **four**[^GestureCount] unique gestures:

 1. Circle
 1. Horizontal Line
 1. V
 1. Z

Each gesture will have **seven**[^GestureTemplateCount] templates recorded.

####Recognizer Test
The participant is asked to perform **each** of the recorded gestures **five**[^GestureRepetitionCount] times to see if the recognizer is able to correctly identify them.  
For each gesture performed, the system will log the scores of each template, the highest scoring template and a timestamp for identification of attempted gesture.
The time and attempted gesture label will be noted by hand and the timestamps logged by the system will be used for identification of attempted gesture.

####Recommender Test
The following configurations will be created by us:

 - **Play / Pause song** using **Circle** gesture in **Home Office**
 - **Skip to next song** using **Horizontal Line** gesture in **Home Office**
 - **Turn lamp1 on / off** using **V** gesture in **Home Office**
 - **Turn lamp2 on / off** using **V** gesture in **Living Room**
 - **Turn lamp3 on / off** using **Z** gesture in **Living Room**

The participant is asked to perform the following actions:

 - Turn on **Lamp1** in **Home Office**
 - Play song on Spotify in **Home Office**
 - Skip to next song on Spotify in **Home Office**
 - Turn on **Lamp2** in **Living Room**
 - Turn on **Lamp3** in **Living Room**
 - Pause song on Spotify while in **Living Room** with the virtual position set to **Home Office**
 - Turn off **Lamp1** in **Home Office**

For each action performed, the system will log the probabilities of all actions for each of the context providers, the outcome (either a single action or a list) and a timestamp for identification of the attempted action.
The time and attempted action will be noted by hand and the timestamps logged by the system will be used for identification of attempted action.

##Evaluation
This section will describe how we plan to evaluate the tests and the data accumulated.

###Gesture Recognizer
####Data Collected
 * Lists of scores of all templates. One list per gesture performed.
 * List of labels of the highest scoring gesture templates

All entries will include a timestamp for when they were logged.

####Success / Failure definitions
**Success**: If at least 80% of the gestures performed were identified correctly as per the definition in [Gesture Recognizer Goal](#gesture-recognizer-goal) then the system works as intended and the test is deemed a success.

###Recommender System
####Data Collected
* Lists of scores of all templates. One list per gesture performed.
* List of labels of the highest scoring gesture templates
* Lists of probabilities of all actions from the GestureContextProvider, one list per action performed
* Lists of probabilities of all actions from the PositionContextProvider, one list per action performed
* Lists of probabilities of all actions, one list per action performed
* List of the action outcomes

All entries will include a timestamp for when they were logged.

####Success / Failure definitions
**Success**: If at least 80% of the actions performed were correct as per the definition in [Recommender System Goal](#recommender-system-goal) then the system works as intended and the test is deemed a success.

[^GestureCount]: We could consider using the same amount of gestures as \$1, \$3 or ¢1.

[^GestureTemplateCount]:We could consider using the same amount of templates as \$1, \$3 or ¢1.

[^GestureRepetitionCount]: We could consider using the same amount of repetitions as \$1, \$3 or ¢1.
