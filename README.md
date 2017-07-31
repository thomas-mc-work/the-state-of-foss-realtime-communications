# The state of FOSS real-time communications

Originally posted by [squaredturtles](https://www.reddit.com/user/squaredturtles) on [reddit](https://www.reddit.com/r/linux/comments/6q5bvt/the_state_of_foss_realtime_communications/).

## Ring.cx

* UI is similar enough to Skype that average user can find their way around

### + Advantages

+ Distributed 
+ Non-webapp clients on all major platforms (except iOS but apparently it's coming at some point) 
+ Allows for fine-grain adjustment of video quality 
+ Excellent NAT traversal 
+ Also, cool: on a network with no internet access Ring clients can find one another and make local calls. 
+ Desktop (at least the Linux one) client has built-in desktop sharing. I've had good luck using this to help fix family members' computers. For the hell of it, I tried watching a video on my phone, which worked better than expected, though the sound was a bit tinny. 
+ Hardware decoded video means my fan is not on constantly during calls (which is the case w/ WebRTC-based solutions) 
+ Multi-party calls work well 
+ Though users might have strange IDs, they don't need to worry about keys. 
* Can easily have multiple Ring accounts in the same applications (e.g., work, personal, etc.) 
* Though many seem to question battery life, I haven't seen that on my phone. It's usually around 1% when idle; a few calls puts it around 5-10%. Not sure how to measure on desktop but, again, it seems less CPU intensive than webRTC solutions. 
* Multi-device support works well. Only need ID and password. 

### - Disadvantages

- Unless using SIP (which isn't default), a user can't accidentally make an call unencrypted. (Which is not the case with Matrix/Riot or XMPP) 
- UI is still a little buggy and has a few strange quirks/choices. 
- It uses lots of data, so really only a solution on WiFi 
- The Windows client is hideous... 
- Maybe I'm too used to looking at projects on Github but it's been hard to follow the development of Ring. They don't update their blog often (I've been following Tuleap and had no idea that 1.0 was near....) 

##Matrix using Riot

* Fairly easy to self-host Synapse 
    * Synapse eats RAM and children even with it's told not to... 
        * This is supposed to get better since Synapse is essentially a rough draft... but I'm not eager to even think about migrating rooms, users, or keys from it to another more efficient server Rust or Go future. 
* Riot feels more like Slack or IRC--which seems, if you just want to have a conversation with a few people, like overkill. It's like having your own forum so you can avoid email. Yeah, sure, it works... 
    * UI is slow and overly complicated. 
* It's really not clear where rooms are located. While a room might appear to be hosted on the Matrix server, if you look at the details of some rooms, they have quite different names and on different servers and you've just joined via an alias. Not a fan. 
* Also not a fan of the nomenclature: @username:server.tld. And many rooms are usefully called ##roomname. 
* Not encrypted by default. Encrypting is laborious. You must create a room, go to "Room Details," then Settings, then encrypt the room. Regular users aren't going to remember those steps. 
    * What's more: only rooms are encrypted, so you can be in an encrypted room and all will be nicely encrypted. But you can also step out of that room into another room, by default unencrypted, have a conversation with the same people before, and now you've lost that protection. 
    * Every time I login through a browser, it seems to add a new device to my profile, each w/ its own key. And you have to navigate into settings before you close your browser and export your keys. Maybe they'll fix all this but honestly, as is, it's a clusterfuck. 
* Video/voice chat works well as does NAT traversal mostly well 
* You're stuck with this webapp bullshit 
    * because of this, one can't live switch between cameras the way you can in other applications 
    * likewise, it doesn't seem to adhere to system volume. 
* Most rooms on the Matrix server actually seem just to bridge already existent IRC rooms. And most of the users in those rooms, since they're on IRC, can't use any of the flashy features that distinguish Matrix from IRC. 
* While you can have multiple identities, you can't use them simultaneously in the same application. 
* No (obvious) way to regulate/delete history of rooms or even delete attachments. 
* Ideally, someone will take the Matrix protocol and make a simple lightweight softphone-like client. Just a contact list, a chat window, and the ability to make calls, share files, etc. Encrypt everything by default. Nothing more. 

## Jitsi Meet

* No software to install; less resistance when asking someone to use it rather than use Skype. 
* Video/audio quality can be quite excellent. 
    * Though tends to deteriorate in quality after an hour or so 
    * It seems they prioritize video over audio; I'd sometimes have excellent 720p video but garbled audio. 
    * They've changed some of bandwidth settings b/c, in the last few months, I've been limited to only audio calls. (Causing me now to use the somewhat clunky but nevertheless consistent WebRTC app in Nextcloud when necessary) 
* Can self-host but pretty heavy 
* Awkward on mobile (though I think there is an app in the Google Play store)

## Mumble

* If setup, clients can be easy enough for tech-illiterate users 
* Easy self-hosting; light on resources 
* Can easily tweak bandwidth to be insanely efficient and still have good quality. Works over 3G maybe lesser networks. (As a side note, while traveling internationally recently, I used Mumble on international roaming over 3G paying per MB, which ended costing around 2-5¢/min compared to 30¢/min for international phone calls. This was by far the easiest/cheapest way to get voice calls in that instance. Even other solutions using Opus don't allow you to dial it down quite so low) 
* While not e2e encrypted, since I self-host I'm OK with that. It still encrypts between client and server. 
* Chat feature is an afterthought. 
* Unfortunately, no video support 

## Signal

* As something that you can tell almost anyone to install it and they can more or less start using it without instruction, it does a lot of things right 
* Disappointed that they yanked encrypted SMS support 
* Though Moxie has been carefully not to say so, I suspect that it will get bought by some company at some point in the future--then, who knows what will happen. Assuming it were to become successful, I cannot see Moxie et al footing the bill for 5+ or 10+ years. Perhaps I'm wrong; perhaps he really is an anarchist. If that were so, I'd expect them to have set up some sort of trust in order to ensure longevity. If they've taken any steps toward that, I haven't seen it. 
* Video/voice work well; no fussing w/ NAT 
* If you have multiple phone numbers, you can only secure one per device. This is absolutely asinine! 
* Also vying for the most bullshit of features is the requirement of a phone number at all. Yes, it allows quick up and running for the mindless but there's no technical reason that there can't be an "advanced" option hidden away so no one accidentally finds its that allow one to register by email. Moxie will cite resources etc, but I call BS. He just doesn't put all his cards on the table, so he's lost my trust. 
* When Twitter bought Whisper Systems, Redphone (precursor to Signal) which targeted dissidents and similar as its users, said users got a month's notice before the service ended: https://www.wired.com/2011/11/twitter-buys-moxie/. Maybe it was Twitter's doing--but Moxie was at least complicit. 

## XMPP

* On the desktop, Jitsi still works surprising well. Yes, it's Java. Yes, it's heavy, slow, convoluted, ugly, etc. 
    * No OMEMO or similar, albeit older OTR 
* Self-hosting w/ Prosody or similar is super easy and has low hardware requirements. 
* Conversations (though I honestly hate the UI) actually gives a quite "professional" user experience in terms of chat--i.e., friends/family have no idea this is one of those 'weird Linux things'. Every time I get one of these multi-party MMSes, I'm thankful to those people I've forced/convinced to use Conversations... 
* It has all the potential to do everything one needs but no one application pulls it all together. There is a fair dose of anti-xmpp sentiment as though it's a failed technology, inefficient and so on but this mars its considerable potential. 
* Can be run over Tor. 
* Monal and ChatSecure on OSX/iOS lag behind Gajim/Android, though are catching up. 
* Jingle voice/video is broken on Gajim; developers haven't seemed intent on fixing. 
* Cool other things like notifications on my laptop using MAX. 

## SIP

* SIP w/ ZRTP or DRTP can be secure. I believe both are e2e. 
* Linphone + Ostel actually gives a pretty good user experience. 
* NAT can still be a pain, even with TURN, and any solution seems network specific. 
* On mobile, Linphone and CSIPSimple work well, but the latter's development is dead (I don't know the status of anything on iOS) 
* Clunky/non-existent file or image exchange; chat features have always been secondary. 
* Self-hosting the server end seems to be a bit more work/headache 
* Has the benefit of allowing unencrypted legacy calls to standard phone-lines 
Edit: I forgot about Tox when I wrote this up--which I suppose speaks for itself. Nevertheless:

## Tox

* The biggest critique against Tox has less to do with the application or protocol and everything to do with the community and development. There once was a considerable amount of enthusiasm here for it and people were donating to buy the then-lead dev a new computer--but they've managed to alienate pretty much all of that. To it's credit, it's tried to clean things up a number of times. But I think it screwed up one too many times. That said, I keep qTox installed and hope it surprises me someday. 
* If text chat is your only goal, it works well enough, though not in any compelling way better than XMPP when self-hosted. 
* The UI of qTox, the most stable and developed desktop client, is easy enough that with a little coaching anyone's mother could figure it out. 
    * The exception might be incoming calls, which are rather small and pushed to the upper-right corner (I only know this because the person I was calling kept telling me Tox never rang. Only later did I realize they never saw the little pop-up.) 
* File transfer works well and fast. This speed is where it trumps XMPP. 
* Calls ring immediately whereas Ring tends to take a few extra seconds before ringing commences. 
* Audio quality has been poor. Video quality even worse. 
* It eats bandwidth. 
* Group messaging is a bit weird but sort of works. 
* While you can share an account across devices, the average person won't be bothered with copy profiles across devices. More problematic, you can't use those accounts simultaneously. 
* Antox, the Android application, has been dropped and picked up again by a new developer so many times I can't even keep track. It also crashes with some frequency. 
