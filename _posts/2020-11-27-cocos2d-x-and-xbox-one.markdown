---
title: Cocos2d-X and Xbox One
date: 2020-11-27 03:59:00 Z
categories:
- Development
- Videogames
tags:
- C++
- Lua
- Xbox One
- Xbox
---

Welcome to our first post. Isn't that exciting? 

I would like to introduce ourselves first.

We're a group of game artists (if we can call ourselves like that). I started developing software a long time ago and have always been in the savvy world of video games, but recently I met a few musicians and a wonderful graphics designer. 

We both resurrected a project that was in the hands of a former member of the group. Sadly he was too ambitious (or too little) to take the project to a whole new level and wanted to take all the credit as "himself" instead of grouping together and creating a collective group along with me.

To make it short, we are now creating games for Xbox platforms because Microsoft has always (and probably will be), pro-developers. I feel super thankful the company has helped us for so long time, indeed, since the now defunct Microsoft BizSpark launch, which gave us all the licenses we required for developing software and running on a Windows machine.

Our next launch is Nino's Future, which, let me tell you, has been a challenge for a couple of years.

Cocos2d-X is a great framework, despite being targeted to mobile platforms, incredible things can be done with it. 

We took the task to port the Lua implementation from the common runtime they offer, with a single drawback, we're locked to the 3.15 version. This has happened since Microsoft offered support, back then and a few years ago, to port the game engine to WinRT, which is, if you don't know, the internal name Windows Store applications have to identify its platform, it is now called UWP, but I believe internally they still use the WinRT name.

If you want to port a video game, disregarding if you use Cocos2d-X or not, I strongly recommend that you follow the SDL path. There are a lot of support, specially for open source video games, which let you compile for the Xbox platforms.

I went through the rush of finding a proper video game to port, to one platform, as quick as possible, and as dirty as it might sound, basing myself on open source technologies. 

I created libcrosswind which is a dead-simple game engine using C++ 17 and SDL2, and I have to tell you, it has a lot of development to be done. It started as an effort to make a few video games possible (such as Sonic, the first Mega Drive release), which I will talk of in future posts, but got overwhelmed by a lot of other technologies that were more mature and ready to go.

Right now we're facing the problem of using internal tools provided by Microsoft for the future being that use DirectX 12, and it's funny because it won't take that much until we see the next generation of consoles, after Series X, time flies, and we have to be prepared to use the next set of tools too.

How we get into Microsoft publishing our video game? I don't even know. They liked the idea. And even our game is a rip-off of a well known video game called Mega Man, which Capcom has refused several times to publish and give us a license to include Mega Man as one of our characters, Microsoft did actually like the idea and said "You're welcome". 

I believe we can supply video games for Microsoft platforms that Nintendo does not provide, or even Capcom itself, and other family focused companies that target Nintendo platforms. We want to get into the market seriously.

Nino's future is available in its early beta stage on our GitHub repositories, if you want to check it out you're free to do so. The video game is a full port for Xbox One and works somewhat good, despite that horrible mouse bug we haven't got the time to fix (the mouse is controlled by the left stick).

All our technologies will target Microsoft platforms as the first instance because we like the company, contrary to beliefs from other companies I've worked with, which launch their first platform to Apple devices complementing they would pay first-come first-served products. We're humble in that aspect and want to deliver video games to the most popular platform in the first place.

Well, that was a pretty long reading. 

Please stay tuned. We will post technical documents, development logs, art, music, and many other game assets that can be a lot of help. We are in the business of open source, and will release some of our code from time to time. I believe it's better to bring more developers to an open ecosystem than rather keeping everything for ourselves and never coming to light.

If you liked this post share it, seriously, share it, it will help everyone.