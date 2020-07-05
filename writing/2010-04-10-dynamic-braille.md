---
layout: page
title: Dynamic Braille
---

###### 2010 April 10<br>
I've had this idea wandering around in the back of my head for almost 10 years, but discussing it with Tom I
realized that I've never taken the time to explain it to anybody or even write it down. <br>
<br>
I want to build a braille computer monitor based on this toy. <br>
<br>
Goals & proposed methods: 
- Dynamic braille text interface - Easy because braille is just a font. 
- 3d rendering of arbitrary GUIs & content - Big software problem 
- Force feedback, genuine touch interface - Hardware problem, GUI design problem 
<br>

Challenges: 
- Frame rate and sudden changes in depth 
- Color, not even gray scale 
- Convert 2d color images to 3d monotone representations 
- Resolution, individual pixel size as well as total screen size 
- Notifying the user that something has changed even when they don't touch it 
- Custom GUI design
- Existing software adaptation

<img src="/images/PinArtToy.webp"/>

<details>
  <summary>Comments</summary>
  
BW: More pins would mean better resolution. But for hardware, pneumatics could drive it, and you could use springs for the return. A mechanism similar to a click pin could lock the pins into "on"or "off" positions. Variable depth would of course be harder. ;-)<br/>
  
CR: Would that allow for 'touch' back-pressure sensors?<br/>

TB: You could use a ton of tiny solenoid switches, giving you electronic control automatically: https://www.youtube.com/watch?v=hsoggQOoG4s<br/>

BW: A solenoid and LVDT have essentially the same guts, so that might work. You'd need to keep each element as radially compact as possible.<br/>

CR: Another crazy idea occurred to me today. What if the individual 'pixels' had an embedded fiber-optic so they could be actual color pixels at the same time?<br/>

BW: That'd make for a crazy cool display, but you're probably not going to approach the resolution of today's flatscreens. Probably best to stick to the original purpose and develop a screen that a blind person might be able to use.<br/>
</details>

<details>
  <summary>Background</summary>
Orriginally posted on Google Buzz. There was a followup post on 2014-08-02 where the comments were pulled from.
</details>
