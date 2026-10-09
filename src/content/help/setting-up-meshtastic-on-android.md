---
title: "Setting up Meshtastic on Android"
description: "A step by step walkthrough of the Android app, with screenshots: LongTurbo slot 14, optional MQTT, and checking your first message with the parrot."
author: "CodePosse"
date: 2026-10-09
tags: ["getting-started", "android", "setup"]
---

This is a plain-English setup guide for the Meshtastic Android app. The goal is to get a new node
working without needing to understand every radio detail first. It was written against Android app
2.8.1 and firmware 2.7.26, so if your screens look a little different, that's probably why.

On an iPhone? There's a separate [iOS version of this guide](../setting-up-meshtastic-on-ios/).

## Before you start

Come say hi on **[Discord](../../discord/)**. The parrot bot there can confirm your messages are
actually reaching the mesh, which is the fastest way to know your setup works.

Some things to expect:

- The mesh can be slow and laggy. Messages drop, you may not see any direct nodes, and replies can
  take a while. It's still fun.
- **Nobody owes you a reply to "test".** Try [node discovery](#9-node-discovery) first. And if you
  don't know your node's ID or have a unique long name, any reply you get could be meant for one of
  the hundred other "test" messages that go out every day.
- Not everyone on the public channel is polite. Some people play a character, some dump random
  text, and some say ugly things. Learn to use the ignore function, it's under
  [advanced functions](#10-advanced-functions).

**Most screens need you to scroll to the bottom and press Save.** Your radio will often reboot and
reconnect after a change. It's annoying, but you should only have to do this setup once.

![The Save button at the bottom of an Android settings screen](../../assets/guides/android/save-buttons.jpg)

*This is the Save button. You'll be pressing it a lot.*

## 1. User settings

Start with your identity. This is how people recognize you and reply to you.

- **Long Name:** something that helps people tell who you are when they reply.
- **Short Name:** 4 characters, or an emoji if you'd rather.
- **Save:** scroll down and press it.

![The Meshtastic Android settings screen, listing User, LoRa, Channels, Security, Device configuration and Module configuration](../../assets/guides/android/0-main-screen.jpg)

*The main settings screen. User is at the top.*

![The User settings screen with the long name and short name fields](../../assets/guides/android/1-user.jpg)

*Long name, short name, then Save.*

## 2. LoRa settings (important)

These control the radio side of things. Start conservative and don't flood the network.

- **Region:** United States
- **Preset:** LONG_TURBO
- **Ignore MQTT:** on
- **OK to MQTT:** on
- **Transmit Enabled:** on
- **Number of Hops:** 3 or 5, so you don't flood the network.
- **Frequency Slot:** make sure it says **14**, or you'll be on your own.
- **Transmit Power:** leave it at 30. There's no benefit to changing it until you know what you're
  doing and have hardware that can make use of it.
- **Save:** scroll down and press it.

![The LoRa settings screen showing region United States, preset LONG_TURBO, Ignore MQTT, OK to MQTT and Transmit Enabled all on, 5 hops, frequency slot 14 and transmit power 30](../../assets/guides/android/2-lora.jpg)

*Region, preset, MQTT, hops and slot. The Frequency Override box shows 908.75 here; slot 14 on
LongTurbo already lands on 908.75 MHz, so you can leave the override at 0.*

## 3. Channel settings

Open your primary channel and use these as a starting point.

- **MQTT Uplink Enabled:** on. This lets public messages your radio hears be passed up to the
  internet.
- **MQTT Downlink Enabled:** off. Turning it on floods the mesh.
- **Position enabled:** on.
- **Location slider:** use this if you have GPS or want to show up on the map. Leave
  **Precise location** off and pick a fuzzy distance.

Press **Save** in the channel box, then **Send** to push the change to your radio.

![The Channels screen with LongTurbo as the primary channel, on slot 14 at 908.75 MHz](../../assets/guides/android/3-1-channels.jpg)

*Tap your primary channel.*

![The channel editor for LongTurbo with MQTT uplink on, downlink off, position on, precise location off and the location slider set to about 2392 feet](../../assets/guides/android/3-2-channels.jpg)

*Uplink on, downlink off, position on, fuzzy location.*

![The Channels screen again, with the Send button now lit up](../../assets/guides/android/3-3-channels.jpg)

*Press Send so the radio gets the change.*

## 4. Device configuration

These make your node behave like a normal user node and help other people identify it.

- **Device Role:** CLIENT. If you're not sure, this is the one. See
  [Best practices](../best-practices/) for when another role makes sense.
- **Node Info Broadcast Interval:** 3 hours. This is what pushes your friendly name out to the mesh.
- **Time Zone:** a GPS radio can work this out. Otherwise, use your phone's time zone.
- **Bluetooth PIN:** change it from the default.
- **Save:** scroll down and press it.

![The Device configuration menu, listing Device, Position, Power, Network, Display and Bluetooth](../../assets/guides/android/4-device.jpg)

*Device configuration. Role and node info are under Device, the PIN is under Bluetooth.*

![The Device settings screen with the role set to CLIENT, the node info broadcast interval at 3 hours, and a time zone filled in](../../assets/guides/android/4-2-device-device.jpg)

*Role, node info interval and time zone. Tap "Use phone time zone" if your radio has no GPS.*

## 5. Position settings

What you set here depends on whether the node moves around or stays put.

**Mobile nodes**, like one you carry with your phone:

- **Broadcast Interval:** 15 or 30 minutes. Shorter means more traffic on the mesh.
- **Smart Position:** on.
- **Smart Interval:** the same as the broadcast interval.

**Fixed nodes:**

- Use **Fixed Position** only on a node that doesn't move.
- Set the intervals much longer, since the location isn't changing.

Then scroll down and press **Save**.

![The Position settings screen with a 15 minute broadcast interval, smart position on, a 30 minute smart interval and fixed position off](../../assets/guides/android/5-device-position.jpg)

*Broadcast interval, smart position and GPS settings.*

## 6. MQTT (optional)

MQTT isn't really mesh in the pure radio sense. It uses the internet to carry your messages, and
the mesh works fine without it. Think of it as a last resort that turns your phone and radio into a
complicated way to send a text.

Only use it if you know why you need it. It can be helpful, but it also defeats the point of
testing how far your radio really reaches. For the full set of our broker settings, see
[How do I uplink to MQTT](../how-do-i-uplink-to-mqtt/).

- **MQTT Enabled:** on, only if you're using MQTT.
- **Address:** `mqtt.socalmesh.org`
- **Username:** `meshdev` and **Password:** `large4cats`. These are the shared public ones for
  our broker, they're meant to be public.
- **Encryption Enabled:** on.
- **Root Topic:** `msh/US/CA/socalmesh` (it's case sensitive).
- **Proxy to Client Enabled:** on if you're using your phone's internet to send messages.
- **Map Reporting:** optional. Pick a vague distance for privacy.
- **Save:** scroll down and press it.

![The Module configuration list with MQTT highlighted](../../assets/guides/android/6-modules-mqtt.jpg)

*MQTT is under Module configuration.*

![The MQTT settings screen with MQTT enabled, address mqtt.socalmesh.org, username meshdev, password large4cats, encryption on, JSON and TLS off, root topic msh/US/CA/socalmesh, proxy to client on, and map reporting on with a distance of about 4787 feet](../../assets/guides/android/6-2-modules-mqtt-config.jpg)

*Server, encryption, topic, proxy and map reporting.*

## 7. Your first message

### Go outside

If you can't see any nodes, give it about 15 minutes and get some height. The top floor of a
parking garage, a hill or any open area makes a big difference. You can also
[scan for nodes](#9-node-discovery).

### Send something worth answering

- Open **Messages** and pick your primary channel (LongTurbo).
- Keep it short.
- Say something unique, so a reply is clearly to you and not to the void. Know your node ID, or
  have a long name nobody else has.

### Check for your node

- Open the **Nodes** page in the app.
- Filter to show direct nodes only.
- If you still see nothing after about 30 minutes, turn the filters off.
- Tried [discovering nodes](#9-node-discovery)?

Nodes may only announce themselves every few hours. Someone can be out there even if they haven't
shown up on your list yet.

![The Conversations screen with a single channel listed](../../assets/guides/android/8-messages.jpg)

*Pick the primary channel. By default it's the only one. (This screenshot was taken on LongFast; yours
will say LongTurbo.)*

![A channel full of short messages from other nodes, with "Say something so replies ID YOU" typed in the message box](../../assets/guides/android/8-testmessage.jpg)

*Say something worth replying to, not just "test". (This screenshot was taken on LongFast.)*

![The Nodes list showing three nodes, with the first one, Meshticles-1w, being the radio this phone is connected to](../../assets/guides/android/8-nodeslist.jpg)

*Pretend Meshticles-1w is you.*

![The Nodes sort and filter menu, with Only show direct nodes ticked](../../assets/guides/android/8-nodes-filtered.jpg)

*The filter options. Tick "Only show direct nodes".*

## 8. Check it worked with the parrot

If you're on the SoCal Mesh [Discord](../../discord/), you can link your node and watch your first
message arrive.

1. Open the Meshtastic app.
2. Go to the **Nodes** page.
3. Tap your node.
4. Copy the **User ID**. It looks something like `!1234abcd`.
5. Go to Discord (general is fine) and type `/linknode`.
6. Paste your node ID into the field.
7. Send a message from the Meshtastic app.
8. Watch the parrot in **Node Monitoring → meshtastic-lt14**. Your message should show up in a few
   moments.

The parrot's post is handy because it shows how many hops your message took to reach it. If you
linked your node and set a long name in step 1, your name shows up too.

![The Nodes list, with your own node at the top](../../assets/guides/android/8-nodeslist.jpg)

*Tap your own node.*

![The node details screen showing the short name, device role CLIENT, node ID and user ID](../../assets/guides/android/8-device-fingerprint.jpg)

*Your node's details. Note the Node ID.*

![The SoCal Mesh Discord channel list, with the Node Monitoring category near the bottom](../../assets/guides/android/8-discord.jpg)

*The Discord channel list. Node Monitoring is near the bottom; look for the lt14 channel.*

![The /linknode command typed into Discord, waiting for a node ID](../../assets/guides/android/8-discord-linknode.jpg)

*Type `/linknode`, paste your node ID and press Enter.*

![A parrot post in Discord showing a message, its hop limit, gateway count, and which nodes heard it at each hop](../../assets/guides/android/8-discord-parrot.jpg)

*If it worked, the parrot posts your message, your name if you linked it, and how many hops it
took. (This one was on the LF20 channel.)*

## 9. Node discovery

The app can scan for nodes around you, on whichever presets you pick, and tell you which one has
the most going on.

**Setting it up:**

- Pick the presets to scan.
- Set how long to scan for.
- Optionally keep the screen on while it runs.

**What you get:**

- A summary of the session.
- Results for each preset separately.
- An analysis of what it heard, with a suggestion for which preset to stay on.
- Results aren't saved to the radio, so screenshot anything you want to keep.

![The Advanced section of settings, with Local Mesh Discovery at the bottom](../../assets/guides/android/9-discover.jpg)

*Settings → Advanced → Local Mesh Discovery.*

![The Local Mesh Discovery screen with Long Turbo ticked, a 15 minute dwell time, keep screen awake on, and a Start Scan button](../../assets/guides/android/9-2-discover.jpg)

*Pick the presets and the duration. The longer the scan, the more likely you are to find nodes.*

![A scan in progress, dwelling on LONG_TURBO with seconds remaining](../../assets/guides/android/9-3-discover.jpg)

*Scan in progress.*

![The scan summary showing 4 unique nodes on LONG_TURBO, channel utilization, RF health, and a recommendation to use LONG_TURBO for this location](../../assets/guides/android/9-4-discover.jpg)

*The results, with a recommendation at the bottom.*

## 10. Advanced functions

**Filtering:** hide messages containing words or patterns you don't want to see.

**Blocking users:** also known as ignore.

**Canned messages:** stored on a radio that has its own screen, like a
[Wio Tracker L1 Pro](https://www.seeedstudio.com/Wio-Tracker-L1-Pro-p-6454.html) or a
[ThinkNode M1](https://www.elecrow.com/thinknode-m1-meshtastic-lora-signal-transceiver-powered-by-nrf52840-with-154-screen-support-gps.html).
They're separated by pipes (`|`) and are a bit limited.

![The Message Filter screen with filtering on and the word quack in the filter list](../../assets/guides/android/11-1-filter-words.jpg)

*Pick words to filter out of your messages.*

![A node's details screen with the Ignore switch under Actions](../../assets/guides/android/11-2-block-user.jpg)

*Tap a node, then flip Ignore.*

![The Canned Message settings, with the messages Hi|Bye|Yes|No|Ok](../../assets/guides/android/11-3-canned.jpg)

*Manage your canned messages.*
