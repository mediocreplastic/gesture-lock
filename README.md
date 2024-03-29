##### Made by: Jaiman Munshi (10), Alex Zhang (10), Nancy Puthenpurayil (11)
##### Made for: APCSA end of year project 2021-2022, Ridge Robotics Club 2021-2022

# GESTURE LOCK

A lock that is unlocked not by a key, or a number wheel, or a fingerprint, but by displaying the right hand gesture or gestures in front of the lock.
A camera embedded in the lock will scan for the right gesture(s).
The code is in python and runs on opencv for the camera and mediapipe's ai hand tracking program.
Any code that doesn't use mediapipe or opencv is 100% original and is made largely in part by Alex Zhang.

Here's How it works:
The gesture passcode is based on binary, where each finger on your hand represents as a binary digit (0/1). A closed fist represents 00000 (0). An open hand represents 11111 (31). A thumbs-up represents 00001 (1). A peace sign would be 00110 (6).

The lock will prompt you to show each gesture in the passcode, and will unlock if you show the right combination of finger binary symbols. Once unlocked, you will have the option to change the password or lock. The new password can be any length > 0. If there are no hands detected when you're prompted to show a gesture, the lock will record a value of -1.

#### Methods:
    getInput
        Called by unlock() and setPw()
        Takes parameter for number of gestures to look for
        Uses mediapipe to get real-time coordinates of each hand landmark
        Calculates the middle of a palm using the coordinates
        Determines a "1" or "0" for each finger on the hand
        Converts the five 0/1's into a decimal number (-1 -> 31)
        Determines the number that the user most likely entered based on the mode of numbers in a certain number of frames of video (30)
        Returns a list of the gestures that the user put in
    setPw
        "Thumbs Up" to activate
        Lock must be unlocked to work
        First use Finger Binary to determine the length of the new password
        Set the password by showing each desired gesture/Finger Binary input after each prompt
        Lock will be locked and the password will be set once completed
    unlock
        "Open Hand" to activate
        Lock must be locked to work
        Show each correct gesture/Finger Binary input after each prompt
        Lock will be unlocked if the input matches the password
        Lock will remain locked if the input does not match the password
    lock
        "Closed Fist" to activate
        Lock must be unlocked to work
        Lock will lock
    flashLED
        Called by getInput()
        Flashed the blue led for 200ms

* NOTE: main.py will only run on the raspberry pi. If you want to run the code on your own computer, use alt.py
