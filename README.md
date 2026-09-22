# Wireless-network-troubleshooting-lab-packet-tracer-
Diagnosed and fixed an SSID visibility fault on a Cisco WRT300N wireless router in Packet Tracer — traced the cause to a disabled SSID broadcast and a LAN/router IP mismatch, then reconnected all clients via wired management.
# Wireless Troubleshooting Lab (Cisco Packet Tracer, SSID Broadcast and Client Connectivity)

`Cisco Packet Tracer` · `WRT300N` · `Wireless Troubleshooting` · `SOHO Networking` · `Help Desk Scenario`

## Overview
This lab simulated a help desk-style troubleshooting call: a customer reported that clients couldn't connect to their wireless network, and that the SSID wasn't even showing up as an available network to connect to. The environment was a small WRT300N wireless router serving a mix of client types (two tablets, a laptop, a wired PC used for management, and a network printer), and the task was to log into the router, diagnose why the network was invisible, and get every client connected.

## Objective
Given a customer complaint of failed wireless connections and a missing SSID, log into the wireless router as an administrator, identify the misconfiguration causing the SSID to be hidden, correct it, and confirm that all wireless clients can successfully connect to the network.

## Environment
- **Router:** WRT300N Wireless Router1
- **Management PC:** PC4 (PC-PT), wired directly into the router, used to access the router's admin GUI
- **Wireless clients:**
  - TabletPC-PT Client 1
  - TabletPC-PT Client 2
  - Laptop-PT Client 3
- **Other device:** Printer-PT Printer (on the network, not part of the wireless troubleshooting itself)
- **Admin credentials:** username `admin`, password `admin`
- **Platform:** Cisco Packet Tracer (.pkt file)

## What I Did

### Reproducing the Complaint
1. Started from PC4, the only device wired directly to the WRT300N, since that's the intended management path into the router's GUI.
2. Opened the router's web-based admin interface from PC4 using the provided `admin`/`admin` credentials.
3. Checked the wireless client devices (tablets, laptop) and confirmed the customer's report: no SSID was showing up in their available networks list, matching the complaint that the network name wasn't visible for connection.

### Diagnosing the Cause
1. In the router's Wireless settings, found that the wireless network (SSID broadcast) had been disabled, which explained why the network wasn't visible to any client trying to scan for it. A disabled SSID doesn't stop the network from functioning, it just stops the router from advertising its name, so clients have no way to find it without already knowing the exact SSID.
2. Also reviewed the IP addressing between the router's LAN side and its DHCP/default settings, checking for the kind of address mismatch that can cause clients to associate with a wireless network but fail to actually pull a usable IP.

### Fixing the Configuration
1. Re-enabled the wireless network / SSID broadcast setting on the WRT300N so the network would advertise its name again.
2. Verified the LAN and DHCP address settings on the router lined up correctly so that clients would receive valid IP addresses on connection, rather than associating with the network but sitting unusable without one.
3. Saved the settings changes on the router.

### Verifying the Fix
1. Returned to the wireless clients (TabletPC-PT Client 1, TabletPC-PT Client 2, Laptop-PT Client 3) and confirmed the SSID was now visible and connectable.
2. Connected each client to the wireless network in turn.
3. Confirmed all three wireless clients had successfully joined the network, resolving the original complaint.

## What's in This Repo
```
wireless-troubleshooting-lab/
├── README.md                          # This file
├── 3.Troubleshooting-Part-2.pkt        # Packet Tracer project file
└── screenshots/
    └── 01-topology-and-scenario.png    # Topology, scenario prompt, and diagnosis notes
```

## Skills I Picked Up
- **Recognizing an invisible-SSID complaint as a broadcast setting issue,** rather than assuming a hardware or association failure, since a disabled SSID broadcast still runs the network, it just stops advertising it.
- **Working from a wired management connection first,** using PC4's direct link to the router to get into the admin GUI, the same pattern a real help desk technician would use when a customer can't reach a device wirelessly.
- **Checking IP addressing alongside broadcast settings,** since a wireless fix that only re-enables the SSID doesn't help if clients still can't pull a valid address once connected.
- **Working a support call scenario end-to-end,** from a vague customer complaint, to root cause, to a verified fix across multiple client devices.

## How This Applies in the Real World
"Wireless isn't working" is one of the most common tickets a help desk or junior network tech will ever see, and a hidden or misconfigured SSID is a frequent, easy-to-miss cause. This lab reflects that real workflow: get into the device the customer can't easily troubleshoot themselves, check the obvious broadcast/visibility setting first, but also sanity-check addressing before declaring victory, since a network that's visible but doesn't hand out usable IPs will just generate a second complaint.

## Where I'm Coming From
I'm making the jump into cybersecurity from a background in **healthcare**. It's a different field on paper, but a lot of the muscle memory carries over: following procedures carefully, protecting sensitive information, staying calm and methodical when something isn't working the way it's supposed to. I'm currently studying for **CompTIA Security+** and building labs like this one to get real hands-on reps in, since that's what I'm missing on paper right now compared to my experience.

## What I Want to Learn Next
- Digging into wireless security settings (WPA2/WPA3, pre-shared keys) beyond just visibility issues
- Practicing MAC filtering and other access-control troubleshooting on SOHO routers
- Getting comfortable with more advanced DHCP troubleshooting (scope exhaustion, reservation conflicts)
- Documenting a troubleshooting process in a ticket-style format, not just a lab write-up

## Limitations & What I'd Do Differently in Production
- **This was a single, pre-built fault scenario.** A real environment could have multiple simultaneous issues stacked together, not just one clean root cause.
- **No packet capture or logging was reviewed** to confirm the SSID and DHCP behavior before and after the fix; in production I'd want log/capture evidence, not just visual confirmation from the client side.
- **Credentials were provided (`admin`/`admin`).** In a real deployment, default admin credentials like these would themselves be a finding worth flagging and changing.

## References
- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
- [CompTIA Security+ (SY0-701) Exam Objectives](https://www.comptia.org/certifications/security)
