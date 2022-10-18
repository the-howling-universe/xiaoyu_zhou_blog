---
title: 'Intro to VR Webinar by Circuit Stream'
date: 2020-08-10 00:00:00
featured_image: '/images/2020-08-10-intro-to-vr-webinar-circuit-stream.jpg'
excerpt: Last week I took part in a free “Introduction to VR” webinar by Circuit Stream, a VR/AR service and training provider that helps companies develop their own apps. This post shares some of my notes from the webinar and thoughts on how I'll proceed from here.
---

Last week I took part in a free [“Introduction to VR”](https://circuitstream.com/workshop/upcoming-live-virtual-reality-workshop/) webinar by [Circuit Stream](https://circuitstream.com/), a VR/AR development training provider and service that helps companies develop their own apps. This post shares some of my notes from the webinar and thoughts on how I'll proceed from here.

![Webinar Screenshot](/images/2020-08-10-webinar-screenshot.jpg)

To begin with, Stephane (the host) told us a little about Unity. He said it’s one of the most popular engines used for creating games, simulations and experiences, and that 60% of XR content is currently made with Unity. He didn’t elaborate on the other 40%, but I suppose it would be a mix of Unreal, other engines, and basic applications such as WebVR.

I’ve heard about Unreal as it’s used in many AAA games and my partner uses it for work. It’s very tempting to learn it because it’s so cool, however, in my personal case, learning Unity first is probably best for me as:
* I currently have a 2013 Macbook Air and Unreal can’t run on macs (even if it could, it wouldn’t run on mine! 😂)
* Majority of the social enterprises I’ve investigated that make VR apps use Unity
* Anecdotally, Unity is easier for beginners. Also, C# is easier to learn than C++ used in Unreal (though Unreal does have Blueprints...)

Stephane also talked a little about headsets that are currently on the market and the best ones for beginner devs to get. His recommendation was the [Oculus Quest](https://www.oculus.com/quest/) as it’s a versatile and affordable option but, if you’ve got the cash, he said the [Valve Index](https://store.steampowered.com/valveindex/) (not officially available in Australia) was the “Lamborghini of headsets”. I’m not at the stage of buying a headset just yet but I’ll probably end up going for the Quest.

From there we jumped into a live dev session with Jerry who showed us how to set up a project for VR, create the XR rig (head and hands), and make a fireball shoot out the hand when pressing a trigger. I’ll share my notes on setting up an XR rig below (using the 2019 version of Unity[^1]) but if you'd like to watch the whole thing you can [access it here](https://circuitstream.com/workshop/upcoming-live-virtual-reality-workshop/).

***
### How to set up a project for VR in Unity:

1. Go to Edit > Project Settings > Player and check the box for “Virtual Reality Supported”. Unity will import the things it needs for working in VR. Oculus and Open VR will appear automatically and it’s possible to add other devices if you wish.
2. Import the package required for the handsets using the package manager. (The package manager has lots of options for adding functionality to projects and is worth poking through.) Go to Window > Package Manager > XR Legacy Input Helper > Install

### How to create the “XR rig” (a representation of the player’s headset and handsets):

1. Create an empty game object in the hierarchy panel and rename it to “XRrig”
2. Create two more empty game objects as children of “XRrig” and name them “LeftHand” and “RightHand”
3. Drag the Main Camera into “XRrig” and rename it “Head”
4. In the inspector for "Head" change “Clipping Plane: Near” to 0.01.

The camera has two clip planes. The farthest one sets the maximum distance the player can see and the closer one sets the position from which the camera starts to render[^2]. There will be an offset between the position of the camera and the near clip plane:

![Position and Offset](/images/2020-08-10-camera-offset.jpg)

This is bad in VR because if the player puts their hand up to their face and it passes through the clipping plane it will not render (ie. their hand will disappear). Changing the “Clipping Plane: Near” position to 0.01 prevents this from happening.

### How to track the movement of the player’s Head, LeftHand and RightHand:

Open “Head” in the inspector, click “Add Component” and choose “TrackedPoseDriver”.<br />
Change the settings to: <br />
Device: Generic XR Device<br />
Pose Source: Center Eye - HMD Reference<br />
Tracking Type: Rotation and Position[^3]

Open “LeftHand” in the inspector, click “Add Component” and choose “TrackedPoseDriver”.<br />
Change the settings to:<br />
Device: Generic XR Controller<br />
Pose Source: Left Controller<br />
Tracking Type: Rotation and Position

Do the same for “RightHand” but select Right Controller as the Pose Source.

### How to assign a mesh object to the hands so we can actually see them:
1. Create a mesh or drag a model from your assets folder and put it as a child under LeftHand or RightHand in the hierarchy
2. In the inspector, set the position to X:0 Y:0 X:0
3. Set the scale to something appropriate (the units are in metres)

Tip: If you only have one hand model, change the X scale to a negative to reverse the model and use it for the other hand.

Now if you play the scene, the objects you have set as the hands will move and rotate as you move and rotate your controller.

***


At the end of the workshop there was a question and answer session. As well as teaching and supporting XR app development, Circuit Stream also build apps for companies so I asked the following question:

> "What are the main roles in a team that develops VR apps? Do people specialise (modeller, coder, project manager etc) or are generalists more common?""

Their answer was as follows:

*"We find that specialists are more common. You need to know a little bit of everything so you can communicate better with your team, but it’s impossible to build a good application by doing everything on your own. There are modellers, programmers, UX/UI specialists, sound designers… but inside these there are even more specialisations like modellers who focus on texturing or environments. People are usually super specialised in this field, but that doesn’t mean you can’t know more things. At Circuit Stream, for example, we have people who are programmers and also designers, but they specialise in one of them. Things are always changing so you need to specialise to be good at something. But it’s always good to know the pipelines and how to communicate with the other team members."*

In my case, I’m totally new to this field so I don’t know for sure what I’ll enjoy most or even be good at. I’ve been thinking that general project management might be my best bet until I’m able to specialise in something (if I decide to do that). I also enjoyed finding ways to automate tasks and improve efficiency in my marketing career, but I feel like that might not constitute an entire role in the kinds of projects I want to get involved with (smaller social enterprises/prototyping). However, learning a little bit of everything is right up my alley and is the best way to figure out what will fit me best.

I was impressed with the workshop and very much appreciated the time the team took to answer everyone’s questions. Circuit Stream’s course is out of my price range and seems better suited to people/companies that have a project they want to work on. However, I’m grateful to be able to access their free webinars and look forward to the next one.

If you'd like to chat to me about this post, feel free to @ me on Twitter via my handle [@aivencha](https://twitter.com/aivencha).

[^1]:Although the 2020 version of Unity is no longer in beta, the tutor recommended using 2019 as it's the most recent long-term support release.
[^2]:The camera’s draw distance sets the maximum distance that can be rendered but it’s possible to tell objects within that scope to not render.
[^3]:Headsets with 6 [Degrees Of Freedom](https://kei-studios.com/quick-guide-degrees-of-freedom-virtual-reality-vr/) (eg. Oculus Quest, PSVR) track both rotation and position. Headsets with 3 DOF only track rotation (eg. Samsung Gear VR, Google Daydream).
