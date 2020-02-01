# R.E.A.L. mod for Grand Theft Auto V - 100% VR!
### by LukeRoss

---

# Table of contents

[Quick setup](#quick-setup)  
[In-game HUD](#in-game-hud)  
[Keyboard/mouse, controller, aiming](#keyboardmouse-controller-aiming)  
[Recentering your view in VR](#recentering-your-view-in-vr)  
[Cutscenes](#cutscenes)  
[Position tracking, animations, and the player's body model](#position-tracking-animations-and-the-players-body-model)  
[I see car wheels in the sky, WTF?!](#i-see-car-wheels-in-the-sky-wtf)  
[Advanced tweaking and hotkeys](#advanced-tweaking-and-hotkeys)  
[More advanced graphics tweaking](#more-advanced-graphics-tweaking)  
[Even more advanced resolution tweaking](#even-more-advanced-resolution-tweaking)  
[Fixes included in the R.E.A.L. mod](#fixes-included-in-the-real-mod)  
[FAQ](#faq)  
[I am an experienced GTA modder and I wish to contribute, where do I begin?](#i-am-an-experienced-gta-modder-and-i-wish-to-contribute-where-do-i-begin)  
[Credits](#credits)

# Quick setup

1. I recommend that you start from a clean installation of the game, updated to the current version (1.0.1868.0), with no other mods present. Then if you wish, after you're confident that everything works correctly in VR with the R.E.A.L. mod, you can try mixing it up with other mods that you like, although I cannot guarantee that there will be no incompatibilities (a sure source of problems for example would be trying to use additional mods that modify the camera FOV). If you're unable to update the game for some reason, old versions down to 1.0.1180.2 should also work, but I can't give you much support there.
2. Before installing the mod, boot up the game normally on your monitor and make the following important adjustments to the settings; when you're done, exit the game again:
```
Settings> Gamepad> Targeting Mode                  : Free Aim
Settings> Camera>  Allow Independent Camera Modes  : Off
Settings> Camera>  First Person Head Bobbing       : Off
Settings> Camera>  First Person Third Person Cover : On
Settings> Camera>  First Person Vehicle Hood       : Off
```
3. Unrar [GTAV_REAL_mod_by_LukeRoss_r4.rar](https://github.com/LukeRoss00/gta5-real-mod/releases/download/r4/GTAV_REAL_mod_by_LukeRoss_r4.rar) into the main game folder, i.e., the one where `GTA5.exe` is, usually something like `C:\Program Files (x86)\Steam\steamapps\common\Grand Theft Auto V`. *Confirm overwrite for all files if you already had a previous release of the R.E.A.L. mod.* Otherwise, there should be no need to overwrite any existing files: if the extraction program asks you to do that, it is probably because you have other mods installed, which you should remove at least temporarily (see point 1).
4. Everything in this step is very important: if you fail to do this correctly, chances are that the R.E.A.L. mod will work very poorly&mdash;or not at all. The game must not be running as you perform these few operations. If you have the Steam version of GTA V, make sure that "Use Desktop Game Theatre while SteamVR is active" is *unchecked* in the game properties page for Steam. Find and run the `RealConfig.bat` file that the mod put into the main game folder. At the prompt, select "High" if you have a high-end system, with a powerful CPU and graphics card, or "Low" if you have a potato computer; try "Medium" if you have a system that runs VR normally and you want to prioritize resolution at the expense of other graphical quality options. The batch file will automatically backup your `Documents\Rockstar Games\GTA V\settings.xml` file as `settings_ori.xml`, and replace it with one of my templates that provide initial graphics settings known to be compatible with the VR mod. Later on, if you are so inclined, you will be able to refine settings to your liking as explained in the [Advanced tweaking](#advanced-tweaking-and-hotkeys) section, in order to find the best possible balance between graphic quality and frame rate.  
**For returning users:** In previous releases of the mod, `settings.xml` needed to be edited manually to specify the correct video card name for your system, and afterwards it was recommended to set the file as read-only. Neither of those hacks is necessary anymore, and in fact it is best *not* to set the file to read-only, otherwise the game won't be able to save your graphics settings if you make changes while playing. Yes, it's now possible to modify graphics options without exiting the game, and you can even enable MSAA! Find out more in [Advanced tweaking](#advanced-tweaking-and-hotkeys).
5. Remember to set your Windows default audio device to the VR headset, otherwise you will have no sound in game (if you have an Oculus system, this step can later be automated with the [Oculus Tray Tool](https://forums.oculusvr.com/community/discussion/47247/oculus-traytool-supersampling-profiles-hmd-disconnect-fixes-hopefully/p1) by creating a profile for GTA V and enabling the Audio Switcher).  
6. Put on your HMD, pick up a gamepad if you wish, launch the game and marvel at the beauty that is Los Santos in VR! Whenever you need to recenter your view or to realign the HUD in front of you, just shake your head once as though you were saying no (more details in the [Recentering your view](#recentering-your-view-in-vr) section below). If tracking seems jerky or jumpy, make sure that ASW (for Oculus) or Motion Smoothing (for SteamVR) is *off*, either globally or for the GTA V app. Looking around with your head should feel perfectly fluid and smooth, just like a native VR game.  
7. If you need troubleshooting, or just want to know more, please read the rest of this file! There is also a [FAQ](#faq) section at the end.

# In-game HUD

After several experiments, I settled on a solution that I believe is the best compromise between ease of access to the various information fields available on the HUD (such as game hints, ammo, subtitles, and especially the all-important radar) and the necessity in VR to keep the HUD out of the way so that it doesn't detract from immersion in the game world.

In my implementation, the HUD is semi-transparent, suspended in space about 3 feet in front of your head, and it is:
1. slightly larger than your field of view in VR, so you'll have to turn your head a little in the direction of the HUD element that you want to observe; this way, your normal line of sight isn't occluded by the HUD elements;
2. fixed in space, instead of somehow rotating after your head with some delay or inertia, a trick used by some games that I personally find very distracting and basically impossible to get right.

A notable exception happens when you are aiming, in which case the HUD will become smaller and headlocked, so you'll always have all the information that you need visible in front of you even when you have to rotate your head quickly to follow enemies.

In the end, if you play sitting on a couch or at your desk, the HUD will always be in front of you, just at the margins of your field of view. If you play in roomscale and you need to turn around, you can reset the HUD position (bringing it again in front of you) anytime you want just by shaking a single no with your head, which will recenter the headset as described in the [Recentering your view](#recentering-your-view-in-vr) section below.   

# Keyboard/mouse, controller, aiming

For my previous [VR conversion](https://github.com/LukeRoss00/nolf2-real-mod/releases) of No One Lives Forever 2, a game that offered no native gamepad support because it was developed before gamepads became common for gaming PCs, I had to come up with custom bindings for the many controls needed. GTA V is way more advanced in that regard, and it will support basically every kind of controller that you throw at it. I have played every mission and activity from "New game" to 100% completion with all Gold medals, fully in VR, using an Xbox One gamepad. There are no special commands needed for VR, apart from the headshake gesture described below to recenter the headset view. Keyboard and mouse will perhaps feel less immersive (the controller vibration does wonders to make you feel like you're actually driving on bumpy roads), but they will also allow you to bring the game to completion. Also, many people are having lots of fun using steering wheels with https://www.gta5-mods.com/scripts/manual-transmission-ikt!!

Oculus Touch controllers (or similar tracked controllers for other systems), however, are NOT supported. There was another mod out there that made them somewhat usable by removing your in-game character's body, but it's not something I'm personally interested in doing, for various reasons:
1. GTA V needs all the buttons you can find on a controller, while Oculus Touch sadly lacks the D-Pad;
2. GTA V is a *long* game, and since the main focus for this mod is being able to complete 100% of the game in VR and to leisurely admire the beautiful and incredibly complex world that Rockstar created, you need to be able to play seated and without holding your arms out in front of you for hours on end. Mimicking a real gun with the Touch controllers can be great fun for a short time, I know, but there is no shortage of gallery shooters to play if that's your bread and butter;
3. perhaps most importantly, both NOLF2 and GTA V were built and designed with traditional FPS aiming in mind. I'm much more interested in preserving the original charm of the games as they were intended to be played, with beautiful animations and precise aiming, than I am in drawing a disembodied, floating gun in the air and perhaps tacking a laser pointer onto it in order to make some sort of aiming possible.

For the same reasons, I went to some effort to implement dominant-eye alignment when rendering the weapon model, so that you can properly aim down the sights as you would in real life. See [Advanced tweaking](#advanced-tweaking-and-hotkeys) later on for information on how to select your dominant eye (default is the right one).

If this is your first time trying out a mod with head-driven aiming, don't let yourself be discouraged by detractors: aiming with your gaze becomes completely intuitive in just a few minutes, it can be done equally well if you play standing in roomscale or seated, and it's way faster and more accurate than aiming with the hand controllers. Again, this is not to say that games built purposely around the Touch system are not fun; they are. However, they do become quite hard on the arms in just a few hours, and as proven by Rockstar's very own partial port of L.A. Noire, that doesn't work so well for vast open-world games.

# Recentering your view in VR

GTA V has quite a few intense moments; so, especially if you move around a lot in roomscale, you may frequently find yourself needing to recenter the view, in particular to reset the HUD to be in front of your line of sight, or to realign the position tracking with the character model (see also [Position tracking](#position-tracking-animations-and-the-players-body-model) below).

You can use the Dash menu by pressing the Oculus button on the controller, or similar overlay menus for other systems; but much more conveniently, you can just briefly shake your head from side to side as if you were saying no. This recentering gesture is always available and recognized, no matter if you're in a mission, free roaming, in the menus, loading the game, and so on. The movement will become second nature in a short while, and I find it so convenient and have become so accustomed to it that I sometimes catch myself doing it in other games and wondering why it didn't work :-)

If you cannot seem to trigger the recentering, follow these instructions:
1. keep your head quite still for a couple of seconds: this is needed because we don't want to have false triggers when you're jerking your head around continuously, e.g. during combat;
2. give a rather sharp shake to the left or the right (a single one is enough, even though the mod can also deal with repeated shakes) and immediately return your head to the initial position. By sharp I don't mean so hard as to hurt your neck or to have the headset slide around on your face: just enough to allow the mod to reliably distinguish the movement from a normal look-around motion;
3. the mod will wait for a fraction of a second to allow your head position to stabilize, and then it will instruct the VR runtime to recenter the headset. There will be no visual or acoustic feedback that recentering has happened, but you'll always be able to tell because the HUD will snap back in front of you (and so will your vehicle if you're in one).

If you are in a vehicle, and you don't need to reset the HUD but only to align your character with the direction the vehicle is facing, a convenient shortcut that won't affect the HUD position is to briefly press the button for looking behind you (defaults to `C` on the keyboard, or pushing in the right stick on the gamepad).

# Cutscenes

**Release 4 update:** *Great news for those of you who like to play the story missions in VR: I finally came up with a universal FOV fix that also works in cutscenes! No more in-your-face characters, no more camera zooms, no more world warping when you turn your head!!*

In my previous [R.E.A.L. mod](https://github.com/LukeRoss00/nolf2-real-mod) for the almost forgotten gem that is NOLF2, I was able to offer a lot of options for viewing cutscenes, so they could be enjoyed by all kinds of people, from those who have built sturdy VR legs down to those who immediately get sick as soon as the camera moves.

GTA V is much more rigid in its management of the camera during cutscenes, ~~and to the best of my knowledge it is impossible to even properly set the cutscene camera FOV from a mod (though if you're a modder and you know different, please see your section further on and get in touch with me)~~. So, cutscenes will be very immersive, but perhaps a little too hard on some players: the camera will ~~zoom in on characters and~~ move around a lot, just as it does in the original 2D version. You'll be able to look everywhere in roomscale and see all kinds of hidden details, however, which should make up for the discomfort!

**Edit:** *This paragraph is no longer very relevant because of the new universal FOV fix, but I'm leaving it here for historical reasons and because it mentions the virtual screen mode, which some people may still want to use.* Release 3 of the mod introduced two different viewing modes for cutscenes. I call the first new mode "dynamic stereo". It automatically adapts to the varying camera FOV, so that the old problem where characters in cutscenes were frequently too close to your face for comfort, and looked somewhat flat, is completely eliminated. It also preserves the ability to look around freely, so for most users it should definitely be an improvement, which made me decide to set it as the new default. The only downside is that, when the camera really zooms in, faces will tend to look larger than life, the same as in 3D movies. If even this way of viewing cutscenes is too much for you, please see the [Advanced tweaking](#advanced-tweaking-and-hotkeys) section below to switch to the second new mode: a static, 2D virtual screen that completely eliminates all issues with motion sickness or vergence, of course at the cost of reduced immersiveness.

Also in [Advanced tweaking](#advanced-tweaking-and-hotkeys), you'll find that there is one option for pitch control that you can modify, and ~~you can even force the FOV, which gets rid of the zoom effect completely but introduces all kinds of artefacts as described in [Car wheels in the sky](#i-see-car-wheels-in-the-sky-wtf)~~[no longer needed]. In case of panic, just remember that all cutscenes can be skipped after a second or so by pressing 'A' on the controller or the left mouse button.

My advice is, if you tend to get sick during cutscenes, just keep very still and don't try to follow or to counteract the motion of the camera with your own head. Also, don't push it: as soon as you start to feel queasy, take a break and don't try again until you feel completely OK. With these simple tricks, you'll build your VR legs in no time!  

# Position tracking, animations, and the player's body model

With NOLF2 I was able to implement full position tracking because the game provided a way to move the main character model accurately by an arbitrary, precise amount. GTA V does not, or if it does, I couldn't find out how. However, position tracking is extremely important for immersion: being able to look around obstacles, for example, or doing stuff like leaning forward and looking up at the moon through your windshield when you're driving around at night, makes the virtual world feel so much more real (R.E.A.L., ha-ha). It makes you feel *there*. So, position tracking is active by default, although it can be disabled as described in [Advanced tweaking](#advanced-tweaking-and-hotkeys).

There's a caveat though. For the technical reasons that I just mentioned, the offset that you apply to the camera when you move your head in real life does *not* directly carry over to your character's head, or body. Actually, if you move around too much while in 1st person, you'll quickly find out that GTA V's body model for the player character does not even include a head! Your character's body ends at the neck with a beheaded stump, and that can be quite disturbing the first few times that you see it. Be advised!

There are also a few circumstances when the game will just take control of the camera, which represents your head, and will make it do whatever it goddamn pleases without heeding your input. That happens for example when you enter a car (as you know, that animation is extra-long if you are committing grand theft auto), when you get thrown from a vehicle, when you slide down a slope, when you roll on the ground, and in other situations of the sort.

All of that can be quite jarring if you haven't yet fully developed your VR legs. Please follow the advice given in the previous [Cutscenes](#cutscenes) section, and as an even stronger recommendation for in-game animations, don't try to fight the camera. Just go along for the ride, let it do what it wants to do, perhaps even close your eyes for a few moments if you feel queasy, and simply wait it out. 

# I see car wheels in the sky, WTF?!

**This section is no longer relevant since I managed to come up with a universal FOV fix! I'm leaving it here for historical reasons and just in case anybody is unable to update to Release 4 of the mod.**

In VR, one of the most important requisites for immersion and to avoid motion sickness is making sure that the FOV (field of view) of the game camera exactly matches the headset's. So, a VR mod has to somehow coax the game into always using the same FOV. The modding community has discovered a few ways to tweak the gameplay camera FOV in GTA V, which made this R.E.A.L. mod possible, ~~but no universal solution has been found, at least that I know of~~.

~~So, even though most of the time I'm able to properly set the camera FOV in a way that allows for correct rendering of all objects, there are situations when I have to forcibly override the field of view during the rendering process itself, which leads to some pop-in at the edges of the image (the game was expecting to draw a narrower portion of the world, so it didn't load some parts of it in time), and most notably to some objects in the world being drawn at the wrong positions. This includes car wheels, suspended wires, shadows and clouds.~~

~~A situation where you'll frequently experience this problem is if you, uh, interact with a hooker in your car. In that case, just concentrate on what happens inside the car, and never mind the wheels floating around outside ;-) Another occurrence of this may be during cutscenes, but only if you force the zoom override as listed further on in [Advanced tweaking](#advanced-tweaking-and-hotkeys).~~

# Advanced tweaking and hotkeys

In the `Grand Theft Auto V\Settings` folder that gets created when you extract the mod, I have provided three template versions of the `settings.xml` file, one of which will be copied over to your `Documents\Rockstar Games\GTA V` directory when you run `RealConfig.bat`, to provide a starting point for your own customized graphics settings.

**Release 4 update:** *It is now possible to modify graphics options without exiting the game, and you can even enable any valid combination of FXAA, MSAA and TXAA! The only thing that still needs to be edited by hand (and kept in sync between `settings.xml` and `commandline.txt`) if you want to change it from my defaults, is the base window resolution. Note that MSAA has a devastating impact on performance, so I only recommend it for people who have powerhouse GPUs (see the new [More advanced graphics tweaking](#more-advanced-graphics-tweaking) section for more info).*

If you want to customize your graphics options to further tune the game performance to your specific system, with the goal of keeping a steady frame rate while at the same time enjoying the fullest graphical quality, there are a few important facts which you should keep in mind. First of all, the settings given in the following table must always be honored for the mod to work properly:   
```
Settings> Graphics>          Aspect Ratio                  : must be Auto
Settings> Graphics>          Shader Quality                : must be either Very High or High
Settings> Graphics>          In-Game Depth Of Field Effects: recommended Off
Settings> Advanced Graphics> Frame Scaling Mode            : must be either 5/2 (x2.500) or 2/1 (x2.000) 
```

The mod also assumes that you are running the game with a square resolution (which can normally be set only in windowed mode). The High and Medium template files use 1080x1080, while the Low one starts from 600x600. Mind that this is *not* the resolution which will be sent to your headset: the mod leverages the internal workings of GTA's RAGE engine to render the in-game world at a much higher resolution, as specified by the `Frame Scaling Mode` value. **Edit:** *see the new [Resolution tweaking](#even-more-advanced-resolution-tweaking) section below for more in-depth information.*

Running the game in a square window is very important, because due to the way VR systems manage the two eye buffers, letting the game choose a 4:3 (or even worse its preferred 16:9) aspect ratio would result in *lots* of wasted pixels, i.e., pixels which would be rendered by the game engine but could never be seen in the headset, causing a big performance loss. You definitely don't want to do that!

*This paragraph is no longer relevant. Since Release 4, all graphics options except for the base window resolution (which can be seen under `Settings> Graphics> Resolution`) can be changed from the in-game menus without breaking the mod.* ~~Unfortunately this also means that most of the graphics settings cannot be tuned while in game, but must be changed by hand in the `Documents\Rockstar Games\GTA V\settings.xml` file after quitting, because although GTA V can work with custom resolutions, it doesn't seem to remember them when it re-initializes the renderer after non-trivial graphics settings have been modified. In practice, what will happen is that GTA V will reset the resolution to 800x600 any time you make a significant change, and the mod will stop working or behave oddly. So, unless I or some other modder manage to come up with a trick to always force the game to use a custom resolution, what you should do is tweak your graphics settings directly by editing the `settings.xml` file after you have quit the game, instead of using the menus. Or, perhaps more easily, you can modify the settings from the game menus, which will revert the resolution to 800x600 after you apply them, and then quit the game and edit the `settings.xml` file to put back the desired square resolution before you launch GTA again.~~

The R.E.A.L. mod offers some advanced options that you can tweak in real time while playing, by using keyboard shortcuts (hotkeys). The hotkeys are disabled by default, to avoid possible problematic interactions with other mods that use the same shortcuts, and also to guard against apparent quirky behavior of the R.E.A.L. mod if the keys get hit inadvertently during gameplay. To enable the hotkeys, press F11. If you want to turn them back off after making your tweaks (the changed options will remain set until you quit the game) just press F11 again. *Note: many people seemed to misunderstand this as a sort of shift key that should be pressed together with the others. That's not the case. F11 behaves as an on/off button, just like Caps Lock.*

Here is the list, with the initial value of each option:
```
F11         Toggle hotkeys - off at start
0           Cycle stereo mode in cutscenes (normal, dynamic, flat screen) - dynamic at start
T           Cycle dominant eye for aiming down sights (none, left, right) - right at start
Y           Cycle heading control (always, only when aiming, never) - always at start
U           Toggle pitch control - on at start
I           Toggle decoupled 3rd person camera - on at start
O           Toggle view matrix fix enable - on at start
J           Cycle pitch mode in cutscenes (absolute, relative, cut relative) - cut relative at start
K           Toggle full camera tracking in cutscenes - on at start
'           Toggle slow motion - off at start
N           Toggle FPS counter - off at start
-           Cycle HUD tracking mode (normal, force fixed, force headlocked, developer) - normal at start
End         Cycle universal FOV fix (never, only cutscenes, only aiming, always) - always at start
NUMPAD /    Recenter HMD - centered at start
NUMPAD -    Toggle VR enable - on at start
NUMPAD .    Cycle zoom override (never, only cutscenes, always except cutscenes, always) - never at start
NUMPAD 0    Toggle position tracking - on at start
NUMPAD 2    Toggle stereo rendering (alternate eyes) - on at start
NUMPAD 3    Toggle darts/tennis FOV override - on at start
```

**Edit:** *since Release 3, the defaults for some of those settings can be customized by editing the* `RealVR.ini` *file. The mod will not overwrite this file, so even if you tweak the options using the hotkeys, the initial values that you set by manually editing* `RealVR.ini` *will be preserved for the next run.*

# More advanced graphics tweaking

Beginning from Release 4, the mod uses a much improved technique for capturing the game's internal rendering buffers. Also, thanks to Reddit users ([/u/SIMBO](https://www.reddit.com/user/SIMBO) and [/u/enarth](https://www.reddit.com/user/enarth)) I found out that forcing a custom resolution in `commandline.txt`, instead of only putting it in `settings.xml`, keeps GTA V from reverting to 800x600 every time that a graphics option is changed.

Together, those two things mean that it is now possible to change graphics settings on the fly while in-game, instead of having to edit the `settings.xml` file manually, which should make finding the perfect compromise between image quality and frame rate much faster and easier than it used to be.

Another new feature of Release 4 is full support for all valid combinations of FXAA, MSAA and TXAA. Now, before you get carried away, there are a few facts that you should keep in mind. FXAA is extremely cheap in terms of performance (it only shaves away a couple of fps) but it doesn't help a lot with shimmering edges, and it also blurs the image noticeably. MSAA is much better in terms of visual quality, but it has a *huge* impact on performance: even just setting it to 2x will burn away more than 30% of your frame rate. This drop is not specific to VR or my mod incidentally: see for instance [this IGN report](https://in.ign.com/grand-theft-auto-v/75164/feature/what-you-see-is-what-you-get-grand-theft-auto-v-edition) from 2015. TXAA looks very good and costs basically nothing, but it only works on NVIDIA cards and in conjunction with MSAA. If you have at least a GeForce GTX 1080 Ti, I suggest the combo MSAA 2x + TXAA for extreme quality: you can win back some of the lost frame rate by dropping Post FX to Normal. On top-of-the-line AMD cards, the best-looking usable combo is probably MSAA 2x + FXAA (I'll need your feedback here, since I cannot test this configuration directly). Do not activate all three on NVIDIA cards (MSAA + TXAA + FXAA) unless you're looking for some sort of placebo gratification: I checked the draw calls and FXAA is internally disabled whenever TXAA is used, even though it still appears as On in the menu.

Last but not least, Release 4 is fully compatible with the latest versions of so-called graphics overhaul mods for GTA V. I have successfully tested NaturalVision Remastered, VisualV, GTA 5 Redux, and M.V.G.A. (Make Visuals Great Again). My personal preference, if you're interested, goes to M.V.G.A., because it gives the most important improvements that you can get from these modifications (less fog with better draw distance and clarity, photorealistic color palette, darker nights) without being so oversaturated and generally a bit over the top as some of the others, and without having any appreciable impact on frame rate. Redux appears to be very buggy, and other modders that I respect said that it's basically [stolen work](https://www.reddit.com/r/GrandTheftAutoV/comments/538pb5/gta_5_redux_stole_visualv_content_visualv_team/), so I'd advise against using it, but if you really must, make sure that you enable some form of antialiasing (either FXAA or MSAA) otherwise 1st person will be broken during nighttime, and set Post FX to Normal otherwise cutscenes will look fuzzy and distorted. Also be mindful that the more realistic lighting conditions that all these mods enable, even though they can look astounding in VR, can sometimes mess with gameplay; for example flying at night becomes much harder and frustrating, especially in 1st person, because you can hardly see the terrain.

ReShade is not compatible with the R.E.A.L. mod and probably never will be, because ReShade is designed to operate on the final backbuffer, instead of the high-res internal buffer that gets sent to the headset. So, if you're installing one of the graphics overhaul mods mentioned in the previous paragraph, skip the optional ReShade installation, otherwise you'll lose fps just to make the onscreen window nicer.

# Even more advanced resolution tweaking

The high-end and medium template files make the game run in a 1080x1080 window, with a frame scaling of 5/2 (`<SamplingMode value="9" />` in the settings file), which means that the actual framebuffer resolution will be 2700x2700. A few users with very powerful video cards, wanting to really push their rendering resolution to extreme values, asked whether it is possible to raise the frame scaling multiplier further: unfortunately it cannot be done, as `<SamplingMode value="9" />` is the maximum. However, what can and should be done if you want to achieve higher supersampling in the VR headset is to increase `-width` and `-height` in the `Grand Theft Auto V\commandline.txt` file, always keeping them identical.

As an example, on the Rift, near-perfect image quality can be obtained by setting both `-width` and `-height` to 1200 before running the game. More than that, especially with MSAA turned on, will bring even the most powerful GPUs available today to their knees and kill your frame rate.

If you are playing with KB/M, and set a base window resolution that is larger than your Windows desktop resolution, you might find your mouse pointer unable to reach all parts of the window, meaning that the menus and some in-game interactions might not work properly. My recommendation in this case is to extend your Windows desktop resolution beyond the limits of your physical monitor, which can be achieved using Dynamic Super Resolution if you have an NVIDIA card, or Virtual Super Resolution if you have an AMD one. I know for a fact that DSR works correctly with GTA V in this context, as I'm using it myself; some feedback would be appreciated from AMD users about VSR.

# Fixes included in the R.E.A.L. mod

Here's an incomplete list of all the stuff that I needed to fix in order to achieve a fully immersive VR environment for GTA V, and to allow playing the game to 100% completion without ever needing to remove the headset (*sorry but this list has not been updated since Release 1, see the release changelogs for the latest news*):  
- 1st person camera while on foot:
	- patched the walking FOV to match the headset's (with updated signatures for game version 1737.6)
	- patched the crouching FOV to match the headset's (again, with updated signatures for game version 1737.6)
	- moved the player character's phone away and to the left, as otherwise it would be way too close to the eye camera and tucked into a corner to be legible
	- tied the character's heading to the direction the player is looking at, so "forward" on the keyboard/controller stick will always correspond to "forward" in the visible game world (selectable)
	- pushed away the weapon models that would otherwise be uncomfortably close to the eye camera (variable offsets depending on the aiming conditions) 
- 1st person camera while in vehicles:
	- patched the FOV to match the headset's
	- we can finally look wherever we want when driving, yay!
- 3rd person camera while on foot:
	- patched the FOV to match the headset's
	- decoupled the camera angles from the position, so that the player can look around with the headset and separately orbit the camera around the in-game character using the mouse/controller  
- 3rd person camera while in vehicles:
	- patched the FOV to match the headset's
- aiming camera:
	- dynamically changed the crosshair depth (distance from the eye) to always match the depth of the object that the player is aiming at
	- recognized when the player is aiming down the sights and moved the weapon so that it aligns with the dominant eye (selectable)
	- applied a special-case treatment when the player is aiming from a vehicle in 1st person
	- applied a special-case fix to the crosshair for armed vehicles (e.g., the P-996 LAZER)
- all cameras:
	- stereoized the world rendering by shifting the in-game camera into the eye positions on alternate frames (see the first question in the [FAQ](#faq))
	- tied the yaw (left/right angle, also called heading) of the in-game camera to the headset's relative yaw
	- tied the pitch (up/down angle) of the in-game camera to the headset's absolute pitch
	- overrode the game's stringent limits on camera pitch, especially in vehicles
	- applied a supplementary view fix during rendering to perfectly correct the camera angles and position even when the in-game camera resists being changed
	- tied the roll (lateral tilt) of the rendering camera to the headset's roll, relative to the vehicle roll when the player is in a vehicle
	- fixed the really close camera coordinates (used e.g. for the player's character body model)
	- fixed the helmet and masks (a special effect applied in 1st person, e.g. when your character is wearing a helmet while riding a bike)
	- provided a way to forcibly override the camera zoom if desired
	- added position tracking so you can look around objects and freely adjust your driving position in vehicles
	- fixed the problematic "look behind" control
	- fixed the yaw control for several corner cases where the game wrestles you for ownership of the camera (sitting on the couch watching TV, climbing ladders, drinking at the strip club, interacting with Chop, swimming, ...)
- cutscenes:
	- adjusted the camera so you can look around freely while a cutscene is playing
	- added position tracking so you can peek around objects
	- recognized scene cuts so the view direction can be reset (adjustable)
	- suppressed the black bars
- HUD:
	- fixed a game issue where if the aspect ratio is not 16:9, the left and right sides of several menu pages would get cut off the screen
- forced the game to use the video card to which the VR headset is attached
- limited the D3D11 maximum frame latency to 1
- fixed heading control while swimming
- fixed the special case for heading control when the player is entering a vehicle
- fixed a number of post-processing effects that would incorrectly be applied to the HUD instead of the eye buffers, like for instance fade-ins and fade-outs, underwater distortion/blurring, ...
- fixed the vignetting effect (used e.g. with rifle scopes)
- fixed the scope border (used e.g. for pier telescopes)
- fixed the yellow and blue markers (used e.g. for race checkpoints and mission locations)
- fixed the golf trails (used to show the ball's predicted trajectory)
- fixed the FOV during darts and tennis games
- fixed the FOV for the fairground rides and the cable car, just check them out!
- fixed the FOV for the cinemas and the strip club
- forced the FOV when you are being entertained by a hooker in your car (some artefacts visible outside the car)
- fixed the darts reticule (the twitching cursor used to aim when playing darts)
- fixed the body bag zipper in Dead Man Walking
- fixed the binoculars effect used in some cutscenes
- fixed some missions that use peculiar ways of controlling aiming (shooting from dinghy, defending Cargobob, ...)
- fixed the erratic camera control when shooting from a heli as a passenger 
- fixed the special HUDs and target markers used in some missions (like Eye in the Sky, Caida Libre, ...)
- fixed the Snapmatic camera shutter effect
- fixed the stunt jumps slow-mo camera
- fixed the 3rd person special camera when mopping the floor in The Bureau Raid
- added an in-HUD fps counter to monitor performance while playing in VR
- detected many special game states (e.g., booting, loading a mission, paused, browsing the in-game internet, using an ATM, closing popups at Life Invader, ...) to bring the HUD in the foreground and adjust the aspect ratio
- added a slow motion control that can be used to make magic moments in VR last (almost) forever

Please note that except for the troubles with the 1:1 aspect ratio and the menus being cut off to the sides, all the above problems are not bugs with the game *per se*, but only issues that stemmed from the VR conversion (similarly to what happens when a game meant for a 2D monitor is coaxed, with the help of 3D Vision, into performing stereoscopic rendering). In truth, I've found GTA V to be unbelievably stable and bug-free, especially when you consider the huge complexity of its open world. 

Also note that when the game is being forced to do something that Rockstar's original implementation would forbid (like looking all the way down toward your feet, especially while in a car) there might be some artefacts and/or camera twitches. The same can happen in cutscenes, particularly if you're looking in a different direction than the game expects.

# FAQ

**Q. *Mmmhhh... When I drive at speed and look sideways, or if I strafe in front of a brick wall, everything looks sort of double... Did I smoke too much weed?*  
A.** Perhaps, I wouldn't know! But seriously, that is an artefact of the alternate-eye rendering used by this R.E.A.L. mod. Stereoscopic rendering, which is essential in VR, would require the scene to be drawn twice as seen from the two eye cameras, and at the exactly same moment. GTA V, however, doesn't allow you to render the world twice without some time passing between frames (and without every moving object/NPC in the world animating), and besides, no PC configuration that I know of would be able to play GTA V at a stable 2x90 = 180 fps with the high FOV, quality and resolution necessary for VR. So, my solution is to render just one eye per frame, and display the previous frame for the other eye; such a trick is sometimes called alternate-eye rendering. Perhaps an example can make this clearer: let's say that at frame 99 the right eye was drawn, and let's call this frame 99R. At frame 100, the left eye will be drawn, and displayed together with the previous rendering of the right eye: 100L - 99R. Then at the next frame time we'll have 100L - 101R, then 102L - 101R, and so on. This means that full frame rate can be achieved in VR with the game engine "only" needing to pump out 90 fps, but it also means that one of the two eyes will always have 11 ms of additional latency, which leads to some doubling of objects that are moving quickly relative to the camera. No doubling will be seen when you rotate your head, however, even if you do it very fast, because I took provisions to have the VR runtime compensate with Asynchronous Time-Warp or reprojection.

**Q. *Okay, that was all very nice and technical, but alternate-eye rendering makes me queasy. Can I disable it?*    
A.** You can disable it, but you will lose the 3D effect (as I said, there is currently no way of achieving 90 fps in stereo with GTA V without alternate-eye rendering). See the [Advanced tweaking](#advanced-tweaking-and-hotkeys) section for instructions. 

**Q. *I can't control/rotate the camera while doing XXX, and also during mission YYY.*  
A.** The game allows you to perform MANY different actions (walking, running, driving, flying, swimming, shooting, shooting while driving, shooting while being driven around by NPCs, playing sports, etc.), and not all of those situations are consistent about the various ways employed to control where you're looking, where you're firing and where you're going. To complicate matters, mission or activity scripts often use their own, peculiar control schemes. I fixed as many corner cases as I could find while going through every mission/variation and activity, so that with the current version of the mod and the game, you should *always* be able to control the camera in VR, usually just by looking around with your head and/or using the mouse or right stick on the controller; sometimes, the left stick might be needed; in rare occasions, one of those controls might be disabled (a notable example is when you are shooting from a helicopter as a passenger: I had to disable headlook because it was too erratic due to the specific behavior of the mission script). So, try looking around with your head, using the right stick/mouse, and/or the left stick; if *nothing* works, please open an issue on GitHub and remember to be very specific about the situation where it happens and any additional mods that you might be using.

**Q. *I hate shitty mods where you have to aim with your head, I'll just wait for a proper one that uses motion controllers.*  
A.** Okay.

**Q. *Smooth turning makes me sick, please add snap turning.*  
A.** At the moment I have no plans to do that, because turning with the mouse or the right stick on the controller is not managed by the mod but by the game itself. Also, I personally find snap turning horrible and immersion-breaking. However, if you are really bothered by smooth turning, you can just play in roomscale and always use your head to look around just like you would in real life; as I mentioned above, through all of the game missions and activities there are only a couple of brief scenes where headlook had to be disabled.

**Q. *Please make a VR mod for game SuchAndSuch 6, I've never programmed in my life but I know it can't be too hard, I believe it shouldn't take more than a couple of hours. I can spare a few bucks if you give me your PayPal.*  
A.** This R.E.A.L. mod, as the one I made for No One Lives Forever 2, was a labor of love. Modding GTA V was actually even harder than NOLF2 (to the point of becoming soul-crushing at times), because it took *a lot* more reverse engineering and trial-and-error, and because the game is so much vaster. I poured all of my free time for almost three months into this project. So no, sorry, I won't mod your game, although I can do consultancy work if you are a serious developer/studio who wants to port an old or new game to VR, and you have a reasonable budget to allocate to the job.

**Q. *I am John Bigcheese with Rockstar Games; I just spoke with Eddie Megaboss at Take-Two Interactive and we decided to send a golden plate to your home address for making one of our flagship games so much more beautiful and for all the additional sales that your mod generated... where do you live?*  
A.** Just PM me! But seriously, I made this mod out of passionate love for the game and the magical world it creates. If it pleases you, that makes me happy; if it interferes with your present or future plans for the game, just ask nicely (no need for any C&D, Rottweiler-lawyer stuff) and I will take it down right away.

**Q. *I'm reckless and I want to feel (well, imagine, perhaps with some help from my USB fan) the wind in my face while I'm driving by setting the camera to "First Person Vehicle Hood", why did you write that I can't?*  
A.** Actually you can, and it *is* kind of exhilarating if you have the stomach for it. The only reason why I'm suggesting to leave that setting Off is that you won't be able to aim by rotating your head while driving and you'll have to use the mouse or right controller stick instead, which makes several missions much harder.

# I am an experienced GTA modder and I wish to contribute, where do I begin?

There are several areas of improvement where the R.E.A.L. mod could really benefit from your input, especially if you know or can find out the answers to these problems:
1. ~~Is there a way to reliably set the FOV for the cutscene camera (either with natives or more realistically by patching the game code)?~~ Yes there is!
2. ~~Is there a way to control the FOV of the main gameplay camera during transitions? The most frequent and annoying transition being the animation where the player character enters a vehicle.~~ Found it!
3. ~~It would be helpful if there was any kind of trick to force the game to always use some specific, non-standard, windowed resolution, to work around the issue where if you change any of the Graphics settings that require the renderer to re-initialize, the game will immediately reset the resolution to 800x600 making the mod unusable.~~ The commandline trick works, thanks Reddit users!
4. This is probably impossible without source access to the game engine, but worth asking anyhow because it's so important: has anybody found a way to render the *same* frame twice, without any change to the world (no time passing between the frames, no advance in animations, etc.) except for the gameplay camera being moved to a different position? This could enable ultra-high-end systems to render both eyes at exactly the same game time, getting rid of the doubling associated with the alternate-eye rendering technique.
5. This one is a *lot* of complex work for relatively little benefit, so only consider it if you love hard challenges and have plenty of spare time on your hands: it would be nice to split rendering of *a.* the really-close objects attached to the camera (hands, weapons), *b.* the player's body and vehicle, and *c.* the rest of the world, into three separate Oculus SDK layers, so that correct ASW/ATW could be applied to each of them, which is especially important for the "stale" eye, i.e., the one that is not being rendered for the current frame. The result could approach the visual quality and stability of simultaneous eye rendering, but again, it's quite a big effort and there are no guarantees. If you want to tackle this problem, and you are knowledgeable about all of the areas involved (GTA modding, 3Dmigoto, and native rendering with the Oculus SDK), please contact me.
6. I've tried several times to fix aiming while the player's in 1st person cover, but new issues keep cropping up, so in the end I gave up and resorted to the "First Person Third Person Cover" workaround. I have a nagging suspicion that the developers put this option in the menu because they too weren't completely satisfied with the implementation :-P If, after looking at the code, you have fresh ideas to make it work reliably (in particular when the player is aiming towards and across the cover, instead of away from it) please let me know.
7. ~~If you are a VR C++ developer with a non-Oculus headset and you want to undertake the semi-arduous work of making a native SteamVR/OpenVR/OpenXR version of the mod, do get in touch and I can give you pointers to get started. It would help *a lot* if you also have experience with the Oculus SDK.~~ Did it myself. Big thanks to [/u/iupvoteevery](https://www.reddit.com/user/iupvoteevery) for lots of testing, support and advice!
8. Does anybody know of a technique (e.g., a native call) to reliably find out when a 1st person animation is being played? For instance, it would be nice to have the option to disable user control of the camera when the character is rolling on the ground during combat (`AI::GET_IS_TASK_ACTIVE(PLAYER::PLAYER_PED_ID(), CTaskCombatRoll)` doesn't seem to ever return true). Note that this is different from ragdolling, which I already know how to detect.
9. Can the non-graphics menu settings (e.g., "Allow Independent Camera Modes") somehow be controlled programmatically or through an .ini file, so that the mod could make the few tweaks it needs at the beginning without user intervention? 

# Credits

This R.E.A.L. mod is a clear case of "standing on the shoulders of giants" if there ever was one. None of this would have been possible without the incredible work of many wonderful communities of people.

First of all, a huge THANK YOU to all the people who contributed, directly or indirectly, to the making of the game itself. It is said that more than a thousand persons worked on GTA V, and that development lasted around 6 years. That would amount to 6,000 person-years invested in the making of this breathtaking alternate world, or 6 person-millennia. Even if that figure might be exaggerated, because it's likely that only a part of those people worked continuously on the game for the whole 6 years, it's still an astounding achievement. There is probably more detail to be found in the game than any single person can fully appreciate or discover.

Next, kudos to the brilliant community of GTA V modders that found and documented a huge chunk of the secret, inner workings of the game engine and of the mission scripts. Without you to open and light the path, making the game work in VR would never have been possible for anyone except Rockstar themselves.

Last but not least, my warmest thanks to the unbelievable community of Shaderhackers who for so many years have taken games programmed to be viewed on a normal monitor and "fixed" them so they could be enjoyed in perfect stereoscopic 3D using the (now sadly moribund) 3D Vision technology. Without their efforts, culminating in the all-powerful tool that is 3Dmigoto, a complex construction like the R.E.A.L. mod would have been just too much work to undertake for a single developer.

I hope that you have loads of fun playing this!!!
