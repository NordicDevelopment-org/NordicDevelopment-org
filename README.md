<div align="center">

# Nordic Development Industries

**Communications infrastructure for when the grid isn't there.**

Mesh networking · off-grid power · rugged field hardware · tactical situational awareness

[midwestmeshlab.net](https://midwestmeshlab.net) — our public community lab

</div>

<br>

## What we build

We design and build the systems that keep people connected, aware of each
other's location, and powered when normal infrastructure isn't an option —
disaster response, remote fieldwork, search and rescue, overlanding, or a
neighborhood that wants a radio network the internet can't take down. In
practice that means two things: **mesh radios that carry a message across
miles with no towers**, and **ATAK, the map that shows a team where
everyone is** once that message arrives.

## Mesh networking, explained

A quick primer, since the terms get thrown around a lot:

- **Mesh network** — devices ("nodes") relay messages for each other instead
  of depending on one tower or router. No single node has to reach the
  destination directly; the message hops node to node until it gets there.
- **Node** — any radio, phone, or computer taking part in the mesh.
- **Hop / relay** — one node passing a message on to the next. More hops
  means the mesh can cover far more ground than any one radio could alone.
- **LoRa** ("Long Range") — a low-power radio technology that trades
  bandwidth for range: often a mile or more between nodes, tens of miles
  with a good antenna and line of sight.
- **Off-grid** — works with no cell towers, no Wi-Fi router, no internet.
  That's the point of everything below.

### Meshtastic

The project most of our mesh work is built around. Meshtastic is free,
open-source firmware for cheap LoRa radios (ESP32/nRF52 boards like the
T-Beam, Heltec, or RAK) that turns them into mesh nodes out of the box —
no license, no subscription, no cell signal required. Pair a node with your
phone over Bluetooth and you get text messaging, GPS position sharing, and
basic sensor telemetry across the whole mesh, with each node extending the
range of every other node.

**Use cases:** group comms on a hike or hunt where there's no cell signal;
keeping a convoy or work crew in contact off-road; a neighborhood or
community mesh that still works when the power and cell towers go down;
event and race-day coordination over a wide area; livestock or remote
equipment monitoring on a property with no connectivity.

### MeshCore

A newer, alternative LoRa mesh firmware, built around dedicated repeater
and "room server" roles rather than every node doing everything. It aims
for more efficient store-and-forward routing on the same class of cheap
LoRa hardware Meshtastic runs on. We track it because the mesh radio space
moves fast, and the right firmware depends on the network you're actually
building — a handful of hikers versus a fixed, permanent repeater network
are different problems.

### Reticulum, NomadNet & MeshChat

**Reticulum (RNS)** is not a radio protocol — it's an encrypted networking
stack that doesn't care what it's running over. The same Reticulum network
can span LoRa, packet radio, Wi-Fi, plain internet, or a serial cable,
automatically routing around whichever paths are actually up. It's the
layer you build applications on top of when you need resilient,
end-to-end encrypted comms and don't want to be locked into one radio.

- **NomadNet** — a distributed, forum-and-mail-style application built on
  Reticulum: nodes host pages, message boards, and file shares that anyone
  else on the network can browse, even with no internet behind it.
- **MeshChat** — a more familiar chat-app experience on top of Reticulum,
  with a web interface for messaging, voice calls, and file sharing between
  nodes.

**Use cases:** secure off-grid messaging that survives losing internet
entirely; bridging mismatched hardware (a LoRa node talking to a laptop
over Wi-Fi, talking to another site over the internet) into one resilient
network; building a custom off-grid application without writing your own
networking layer from scratch.

We keep a full walkthrough for standing up Reticulum, NomadNet, and
MeshChat yourself in **[SETUP-GUIDE.md](SETUP-GUIDE.md)**.

## ATAK — tactical situational awareness

**ATAK (Android Team Awareness Kit)** is the other half of what we build.
Where Meshtastic and Reticulum get a message across distance, ATAK is the
shared map that message shows up on. Originally developed for the military
and now released in a civilian version (CivTAK/ATAK-CIV), ATAK runs on a
phone or tablet and gives a team a live, shared picture: everyone's
position, markers for points of interest or hazards, drawn routes, chat,
and file sharing — all overlaid on offline maps that work with zero
connectivity.

The real power of ATAK shows up when it's paired with mesh radio: a
Meshtastic node feeding position and message data into ATAK means a team
knows where everyone is and can talk to each other with no cell network
and no internet, anywhere the mesh reaches.

**Use cases:** search and rescue teams tracking who has covered what
ground; wildland fire crews maintaining shared awareness of fire lines and
personnel; event security and venue operations; off-grid group travel and
overlanding where knowing everyone's position matters; any team-based
field operation where "where is everyone, right now" is the actual
problem being solved.

This is where our device-provisioning and launcher tooling lives — getting
the phones and radios that run ATAK in the field configured and ready to
go, not just the software on a shelf.

## Featured project — Midwest Mesh Lab

[**Midwest Mesh Lab**](https://midwestmeshlab.net) ([source](https://github.com/NordicDevelopment-org/Midwest-Meshlab-site))
is our open community hub for off-grid mesh networking, Raspberry Pi
builds, and open hardware across the Midwest. It's where the region's
Meshtastic and mesh-radio community trades builds, node maps, and
troubleshooting notes — and it runs on a "no invented content" policy:
nothing gets published there until it's real. We hold ourselves to the
same standard here.

## This repository

This is our GitHub org profile — the page you're reading is what shows up
when someone visits [github.com/NordicDevelopment-org](https://github.com/NordicDevelopment-org).
Alongside this README, it also holds **[SETUP-GUIDE.md](SETUP-GUIDE.md)**,
a complete, standalone walkthrough for building your own Reticulum /
NomadNet / MeshChat setup on Windows, macOS, Linux, or a Raspberry Pi.

## Projects we build

**Mesh communications**
| Project | What it is |
|---|---|
| [Meshtastic-Solar-Node-Build-List](https://github.com/NordicDevelopment-org/Meshtastic-Solar-Node-Build-List) | Hardware list for a full off-grid, solar-powered Meshtastic node |
| OffGridCommsStack | Several comms tools (Meshtastic, Reticulum, and more) integrated onto a variety of hardware |
| meshchat-docker | Containerized deployment of Reticulum MeshChat |
| rugged-radio-production | Build and production system for our Rugged Radio mesh devices |
| Meshnet | Dashboard for keeping an eye on mesh and comms activity |

**ATAK & field devices**
| Project | What it is |
|---|---|
| device-provisioning | Provisioning tool for setting up the EUDs (end-user devices), DARTs, and other field hardware that run ATAK |
| Gotak-Launcher-APK | Custom ATAK launch-screen APK |

**Off-grid power & hardware**
| Project | What it is |
|---|---|
| Offgrid-Power-Configurator | Configure an auxiliary off-grid power system and get pricing, a cutlist, and a components BOM |
| Cutlist-Configurator | Configurator for wire size, color, length, terminal type, and terminal locations |
| AustereEssentials | Curated, portable reference toolkit for a PACE plan — for when the internet isn't there |

**Community & lab**
| Project | What it is |
|---|---|
| [Midwest-Meshlab-site](https://github.com/NordicDevelopment-org/Midwest-Meshlab-site) | Source for [midwestmeshlab.net](https://midwestmeshlab.net) |

Most of the above are private, working repos rather than public releases —
we build them for our own use and for direct client work. There's also
internal tooling and experiments not listed here. If you're working with
us, you already have access to what you need.

## Stack

`Python` · `Meshtastic` · `Reticulum` · `LoRa` · `ATAK` · `Raspberry Pi` · `JavaScript` · `Docker`

## Get in touch

Questions about a project here, or want to talk mesh networking? Open an
issue on the relevant repo, or start at [midwestmeshlab.net](https://midwestmeshlab.net).

<div align="center">

<sub>Built for the field, not the demo.</sub>

</div>
