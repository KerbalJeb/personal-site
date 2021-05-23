---
layout: single
title: "Alarm Clock Project"
collection: projects
header:
    teaser: /assets/images/alarm-img.jpg
pcb_gallery:
    - url: /assets/images/alarm-img.jpg
      image_path: /assets/images/alarm-img.jpg
      title: "Final Alarm"
    - url: /assets/images/AlarmExploded.png
      image_path: /assets/images/AlarmExploded.png
      title: "Exploded view of laser cut case"
    - url: /assets/images/alarm-sch.png
      image_path: /assets/images/alarm-sch.png
      title: Schematic
    - url: /assets/images/alarm-pcb.png
      image_path: /assets/images/alarm-pcb.png
      title: "PCB Layout"
---
My second year design course consisted of designing an alarm clock using an Arduino Uno with a partner. Unfortunately, I had to complete this class online so the majority of the project was done using a state of the art circuit simulator and CAD package known as *TinkerCad* (it is really quite awful). The PCB design was done in KiCad which is actually not terrible, no where near as nice a Altium but getting close to Eagle. Fortunately, I was able to use SolidWorks for the CAD portion of the project (designing a case to be laser cut) and was able to create a physical version of the alarm clock with my partner on my own time. Some images of the completed alarm clock and design files are shown below. The main note worthy feature of it is that the LCD backlight will automatically adjust to the ambient light.

{% include gallery id="pcb_gallery" %}

The project source files and final report are available on my [GitHub](https://github.com/KerbalJeb/ECE299DesignProject/releases/tag/V1.0) under releases.
