---
uuid: b5407449-8ebb-45c8-882c-bf4b0fe619fe
share: true
---
###### **Superhero iPhone App for People with ADHD**


* By: Courtney
* Ever forget you had food in the Oven or brush your teeth, this app is supposed to help you with that
* A expertly crafted chatbot with curated user tested [[Prompt Ecology]] designed to help manage your behaviours
* The AI assistant help you makes plans then sets reminders to help hold you to them, but not too tightly

###### **Merged code into [[Ublock Origin]] to block Youtube Ads**

* [By: Smitty](https://iter.ca/)
* Made it on the [frontpage of hacker news](https://news.ycombinator.com/item?id=44329712)
* You can use a Google Developer account to get a special URL that will put ads on a youtube video every time you watch it
* Turns out the videos on Youtube are not from youtube but some Google [[CDN]] product. This [[CDN]] has caches in many popular [[ISP]]'s, the demo showed the youtube video coming from a [[Rogers Communications]] IP address, while on a [[Rogers Communications]] Internet Connection
* The technique youtube uses to block ad blockers uses/used JSON.stringify to validate some info, but if you overwrite JSON.stringify with the same function except it does a string replace, you can fool the youtube script to provide the direct video link rather than one with an ad
* That method was patched, luckily there is this [Javascript Proxy Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) that somehow keeps our ad blockers working read the PR for more details
* Link to [Github Comment](https://github.com/uBlockOrigin/uAssets/issues/27415#issuecomment-2964564722) that was merged
* And yes, this code is running on millions of of computers including [[Brave Browser]] which just rips its filter lists from [[Ublock Origin]]

###### **Programmable Split Keyboard**

* [By Pavelz](https://github.com/pavelz)
* Epic Keyboard that can be configured via a web browser that uses WebUSB
* The keyboard can be configured to act as a mouse using the [[vim]] key bindings
* Special keys can be used to remap the entire keyboards keys, [[Dvorak]] anyone?
* The Product: [The keyboard]([https://www.aliexpress.com/item/1005008130501852.html?spm=a2g0o.order_list.order_list_main.20.53771802lEUpmy](https://www.aliexpress.com/item/1005008130501852.html?spm=a2g0o.order_list.order_list_main.20.53771802lEUpmy "https://www.aliexpress.com/item/1005008130501852.html?spm=a2g0o.order_list.order_list_main.20.53771802lEUpmy")) , [config interface]( https://vial.rocks/)

###### **iPhone App Full Stack Instagram Clone**

* [By Pavelz](https://github.com/pavelz)
* Custom implemented backend even including Authentication
* Logo is an omage to the old, and better, instagram logo
* App is using raw Swift, no webapp as a native app shenanigans
* Source Code: [pavelz/instapicture](https://github.com/pavelz/instapicture)

###### **[Brivo](https://briove.com/) contact management app**

* By: Dimitri
* Take a photo of a business card, have AI extract the information, and save it as a [[vCard]] in the app
* The app gives users a custom URL just like [[Linktree]]
* Brivo supports adding reminder's that will notify you to follow up with a contact
* Add tags to your contacts
* Built with [[Context.dev]] backend
* [Link to Brivo app](https://briove.com/)



###### **[[Claude AI]] Chat Export and Analysis**

* By: Kromar
* Demoed exporting all their personal [[Claude AI]] chat logs
* Demoed loading all that JSON into [[Power Query]]
* Showcased how to filter chat logs to find the most notable ones, for example most chat logs don't have a title
* SOURCE CODE

###### **Custom Music Scale with [[PyGame]] Interface to Play It**



* By: Valentin
* Presented slides explaining how resonance and music scale note frequencies are generated
* Showed how resonance in synthetic music generation works, and how it can be played with
* Demoed a PyGame application and playing a new type of musical instrument
* LINK TO SLIDES, LINK TO CODE

###### **[cenutrytale.com](http://cenutrytale.com/) AI Image to Video Interface**

* [By: Masa](https://www.linkedin.com/in/masatoshi-nishimura-724365183/)
* A website where users can upload photos and animating them with a text prompt for guidance
* The interface made it easy to view the same image animated against different prompts back to back
* We discussed value of animating old back and white photos for use in museums
* Link To Site
* Site: [cenutrytale.com](http://cenutrytale.com/)