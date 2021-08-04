# The Smart Farming Project

## Overview
Smart farming is about integrating smart things like smart farm equipment, sensors, data analytic agents, knowledge graph etc. for the purpose of assisting the farmer to improve the productivity. Reducing or avoiding ecological damage is also a topic which smart farming attempts to address. This domain reveals to us a wide range of concepts and technologies that can be put to use. Idea for interactions!

## It all started with this hackathon...
Inspired by two [robots](https://shop.m5stack.com/products/lidarbot-mecanum-wheels?variant=16804788895834) which are equipped with LiDar sensor and Mecanum wheels (can move sideways), and yet another tiny and less capable [robot](https://shop.m5stack.com/products/roverc-prow-o-m5stickc?_pos=1&_sid=88fd6a8bb&_ss=r), we thought about a scenario where flexible navigation and obstactle recognition would be cool to demonstrate. And then, Simon told us about the smart tractors stuff. So..

### The setup
Farmer Moore owns three smart tractors whom he lovingly calls *Spock*, *Uhura*, and *Sulu*. He also has a drone with a camera (hoverbot called *Mea 3*) which can tell him whats going on on his field. Their features are:

#### Spock
* Can move (forward,backward, left and right sideways, rotate around vertical axis)
* Can scan the environment using LiDar. 12cm height, 270 degrees view.
* Has a soil condition sensor which provides soil moisture, pH, and iron content (well, faked using a [color and reflectivity sensor](https://shop.m5stack.com/products/color-unit?_pos=1&_sid=cdd8120fb&_ss=r)).
* Has irrigation and fertilization tanks (faked using LEDs) which can dispense water and fertilizer. However, these cant be used when sensing soil conditions.
* Is powered by battery whose level can be queried. Also its motor temperature can be queried.

#### Uhura
* Can move (forward,backward, left and right sideways, rotate around vertical axis)
* Can scan the environment using LiDar. 12cm height, 270 degrees view.
* Has large irrigation and fertilization tanks (faked using LEDs) which can dispense water and fertilizer.
* Is powered by battery whose level can be queried. Also its motor temperature can be queried.

As you see, Uhura just lacks the soil sensor. But then she has a larger water and fertilizer tanks.

#### Sulu
* Can move (forward,backward, left and right sideways, rotate around vertical axis)
* Can scan the environment using LiDar. 12cm height, 270 degrees view.
* Can grab and pull out weeds. But you need to tell it exactly where the weed is.
* Is powered by battery whose level can be queried. Also its motor temperature can be queried.

(We will soon add an orientation sensor to these robots to ease the navigation control)

#### Mea 3
* (Faked using a batter-powered WLAN camera stuck on the ceiling)
* Can take HD resolution picture of the field, or can stream mjpeg video.
* Is powered by battery, and not a big one that too.
* Can only recognize the tractors and its position and orientation. Not the plants and weeds, or the soil condition.

#### The farm
* Blocks of wood (from a [game](https://www.galaxus.ch/de/s5/product/goki-wikingerspiel-strandspiele-6429425)) simulates plants and weeds.
* Colored paper sheets under the blocks represent the soil condition.
* The boundary of the farm is marked by pegs

### The problem

Plants must be nourished. If the soil indicates lack of moisture (red paper) then it needs to be watered, or if it needs fertilizer (yellow paper) then it needs to be fertilized. Healthy soil is green. Soil conditions change with time (someone replaces the paper sheets). *Spock* can detect soil condition.

Weeds will crop up all over the place. You need to locate and remove them. Watering or fertizling soil which as weeds is not a good idea. *Sulu* can remove weeds, but needs guidance.

Plants can come and go. You need to survey the field and keep the count updated.

If the tractor battery runs out or its motor gets overheated its going to breakdown. Better not let this happen because Moore has to tow it back.

If *Mea 3* runs out of battery, it will crash. Big problem.

If you cant figure out something, or need Moores assistance, you should contact him.