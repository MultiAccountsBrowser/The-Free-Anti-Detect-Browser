# WebRTC Fingerprint Test: How to Measure WebRTC Browser Signals

WebRTC is a browser technology designed for real-time communication, including audio, video, and peer-to-peer data connections.

Because WebRTC interacts with network interfaces and browser APIs, websites can inspect certain WebRTC-related information. This makes WebRTC an important area to examine when evaluating browser privacy, proxy configurations, browser profiles, and fingerprint consistency.

This guide explains how to test WebRTC behavior systematically.

The objective is not to claim that a browser is completely private or "undetectable." Instead, a good WebRTC test should answer practical questions:

* What network information does the browser expose?
* Does the result remain consistent across repeated tests?
* Does changing the proxy affect the observed behavior?
* Do separate browser profiles behave as expected?
* Does browser configuration change the result?
* Does the browser expose information that was not expected?

For the broader fingerprint-testing framework, see [Fingerprint Tests](./fingerprint-tests.md) and [Test Methodology](./test-methodology.md).

---

## What Is WebRTC?

WebRTC stands for **Web Real-Time Communication**.

It provides browser APIs that allow web applications to support real-time communication without requiring a traditional plugin.

Common applications include:

* Video calls
* Voice calls
* Screen sharing
* Peer-to-peer communication
* Real-time collaboration
* Browser-based conferencing

WebRTC can interact with the browser's network stack and local network interfaces.

As a result, WebRTC behavior can be relevant when testing browser privacy and network configuration.

---

# What Is a WebRTC Fingerprint?

A WebRTC fingerprint is not necessarily a single identifier.

Depending on the test and browser implementation, a website may observe information related to:

* Network interfaces
* IP address candidates
* Connection characteristics
* WebRTC capabilities
* Browser-supported APIs
* Media device information
* Peer connection behavior

The exact information available depends on the browser, operating system, permissions, browser configuration, and website implementation.

Therefore, WebRTC should be treated as one component of a larger browser and network environment.

---

# Why Test WebRTC?

WebRTC testing is useful for several reasons.

### 1. Privacy testing

A test can reveal what network-related information is exposed to a website.

### 2. Proxy testing

WebRTC behavior can be examined alongside a proxy configuration to understand whether the browser exposes unexpected network information.

### 3. Browser profile testing

Separate browser profiles can be tested to determine whether their configurations behave consistently.

### 4. Fingerprint research

WebRTC can be evaluated as one component of a larger browser fingerprint.

### 5. Automation testing

Automated browsers can be tested to determine whether their WebRTC behavior differs from normal browser sessions.

---

# WebRTC Test Architecture

A simplified model looks like this:

```text id="8y4k4x"
Website
   ↓
WebRTC APIs
   ↓
Browser Network Stack
   ↓
Network Interfaces / Connection
   ↓
Observable WebRTC Information
```

This is different from Canvas or WebGL testing.

Canvas and WebGL primarily examine graphics-related browser behavior.

WebRTC testing focuses more heavily on browser networking and communication capabilities.

---

# What Should You Record?

A useful WebRTC test should document the environment.

Record at least:

| Variable         | Example                  |
| ---------------- | ------------------------ |
| Date             | 2026-09-04               |
| Browser          | Chromium-based           |
| Browser version  | Version number           |
| Operating system | Windows                  |
| Profile          | Profile A                |
| Proxy            | Proxy configuration      |
| Network          | Test network             |
| WebRTC result    | Observed result          |
| Test website     | WebRTC test              |
| Notes            | No configuration changes |

For advanced testing, also record:

* Proxy type
* Proxy location
* Local network configuration
* Browser permissions
* WebRTC-related browser settings
* VPN status
* IPv4/IPv6 environment
* Headed/headless mode
* Automation framework
* Profile configuration

---

# Establish a Baseline

Start without changing multiple variables.

For example:

```text id="6b5wqf"
Browser:
Chromium Version X

OS:
Windows

Profile:
Profile A

Proxy:
None

WebRTC Observation:
Result A
```

Run the test several times.

```text id="z5k6gc"
Run 1 → Result A
Run 2 → Result A
Run 3 → Result A
Run 4 → Result A
```

Now you have a baseline.

---

# Test WebRTC Repeatedly

One test run is not enough to establish stability.

Run the same test multiple times without changing the environment.

Example:

```text id="6w0s8e"
Run 1 → Candidate Set A
Run 2 → Candidate Set A
Run 3 → Candidate Set A
Run 4 → Candidate Set A
Run 5 → Candidate Set A
```

If the result changes:

```text id="x4b7zq"
Run 1 → Candidate Set A
Run 2 → Candidate Set A
Run 3 → Candidate Set B
```

investigate what changed.

Possible factors include:

* Network changes
* Browser restart
* Proxy changes
* VPN changes
* IPv4/IPv6 availability
* Browser configuration
* Permission changes
* Operating-system changes

---

# WebRTC and Proxies

Proxy testing is one of the most useful WebRTC experiments.

A proxy affects how browser traffic is routed, but WebRTC may involve additional network mechanisms.

Therefore, do not assume:

> "The browser is using a proxy, so every WebRTC-related network signal must automatically match the proxy."

Instead, test the actual browser.

A controlled experiment might look like:

```text id="f1g4k6"
Test A
Proxy: None
WebRTC: Result A

Test B
Proxy: Proxy 1
WebRTC: Result B
```

Then repeat the experiment.

```text id="3y6j4m"
Test A
Proxy: None
Run 1 → Result A
Run 2 → Result A

Test B
Proxy: Proxy 1
Run 1 → Result B
Run 2 → Result B
```

The results provide evidence about the specific browser and network configuration being tested.

---

# WebRTC Does Not Equal Your Proxy IP

One of the most common misunderstandings is assuming that a proxy automatically defines every network identity visible through the browser.

A browser environment can involve multiple networking layers.

For example:

```text id="z1m2yb"
Browser
   ↓
Proxy
   ↓
Internet

WebRTC
   ↓
Browser Network Interfaces
   ↓
Connection Infrastructure
```

The exact behavior depends on the browser and network environment.

This is why WebRTC should be tested rather than assumed.

---

# IPv4 and IPv6

Network environments may support:

* IPv4
* IPv6
* Both
* Neither in certain configurations

When testing WebRTC, document the network environment when relevant.

For example:

```text id="n3e0h9"
Network A
IPv4 → Available
IPv6 → Disabled

Network B
IPv4 → Available
IPv6 → Available
```

Different network configurations can produce different observations.

If you are comparing two WebRTC tests, make sure the underlying network environment is understood.

---

# WebRTC and Browser Permissions

Some WebRTC functionality involves permissions.

For example, websites may request access to:

* Microphones
* Cameras
* Other media devices

A test should record whether relevant permissions were granted, denied, or not requested.

For example:

```text id="2k9p8n"
Microphone Permission: Denied
Camera Permission: Denied
WebRTC Test: Result A
```

Then compare against another controlled state if necessary.

---

# WebRTC and Media Devices

Browser environments can expose information related to media devices through browser APIs.

Depending on permissions and browser behavior, this may include:

* Number of devices
* Device types
* Device labels
* Device identifiers

The exact information available varies by browser and permission state.

Therefore, media-device testing should always document the permission state.

---

# WebRTC and Browser Profiles

Browser profiles can maintain different browser state and configuration.

When testing multiple profiles, test them independently.

Example:

| Profile | Proxy   | WebRTC Result |
| ------- | ------- | ------------- |
| A       | Proxy A | Result A      |
| B       | Proxy B | Result B      |
| C       | Proxy C | Result C      |

Then repeat:

```text id="c5t6u4"
Profile A → Result A
Profile B → Result B
Profile C → Result C
```

The goal is to determine whether each profile behaves consistently according to its configuration.

---

# WebRTC and Browser Restarts

Restart testing is useful because browser state and network conditions can change.

Example:

```text id="d8z1m4"
Before Restart:
Result A

After Restart:
Result A
```

If the result changes:

```text id="1y5r7c"
Before Restart:
Result A

After Restart:
Result B
```

investigate the environment before drawing conclusions.

Possible causes include:

* Network changes
* New IP assignment
* Browser configuration
* Proxy reconnection
* IPv4/IPv6 differences
* Permission state
* Browser version changes

---

# WebRTC and Browser Versions

Browser updates can affect WebRTC APIs and network behavior.

Record the exact browser version.

For example:

```text id="g0t9c5"
Browser 140
WebRTC → Result A

Browser 141
WebRTC → Result B
```

This is a useful observation that can be investigated further.

Without browser-version information, historical WebRTC test results are difficult to reproduce.

---

# WebRTC and Operating Systems

Different operating systems can have different network and device environments.

A controlled cross-platform experiment might look like:

```text id="q3p1v9"
Windows → Result A
macOS   → Result B
Linux   → Result C
```

Do not assume that the operating system is the only reason for a difference.

Network configuration, browser version, permissions, and hardware can also matter.

---

# WebRTC and VPNs

A VPN and a proxy are not identical technologies.

A VPN generally operates at a different networking layer from a browser-configured proxy.

When comparing them, document the actual configuration.

For example:

```text id="3s6d2k"
Test A
VPN: Off
Proxy: Proxy A

Test B
VPN: On
Proxy: Proxy A
```

If WebRTC observations change, the experiment provides evidence that the networking environment matters.

For a broader explanation of proxy and VPN differences, see [Proxy vs VPN](../proxy/proxy-vs-vpn.md).

---

# WebRTC and Browser Fingerprinting

WebRTC is only one part of a larger browser environment.

Other potentially relevant signals include:

* Canvas
* WebGL
* Audio
* Fonts
* GPU
* Screen characteristics
* Browser properties
* Network information
* Cookies
* Session state

A useful model is:

```text id="5f6u3a"
Browser Environment
       ↓
 ┌─────┼──────────┐
 ↓     ↓          ↓
WebRTC WebGL    Canvas
 ↓     ↓          ↓
Network GPU     Rendering
       ↓
Combined Browser Signals
```

For the complete fingerprint picture, see [Browser Fingerprinting](../docs/browser-fingerprinting.md).

---

# WebRTC Testing With Automation

WebRTC behavior should also be tested when browsers are controlled through automation frameworks.

Common tools include:

* Playwright
* Puppeteer
* Selenium

Record the automation environment.

Example:

```text id="8c4m2p"
Browser:
Chromium

Automation:
Playwright

Mode:
Headed

Profile:
Test Profile

Proxy:
Proxy A

WebRTC:
Result A
```

Then compare it with a manually launched browser.

```text id="q9s7v2"
Browser:
Chromium

Automation:
None

Mode:
Headed

Profile:
Test Profile

Proxy:
Proxy A

WebRTC:
Result B
```

If the observations differ, investigate the configuration instead of assuming that automation alone caused the difference.

---

# Headed vs Headless WebRTC Testing

A useful controlled experiment can compare headed and headless execution.

```text id="3p9j2x"
Headed
→ WebRTC Result A

Headless
→ WebRTC Result B
```

If the results differ, record the difference and investigate.

Relevant variables may include:

* Browser version
* Browser launch configuration
* Permissions
* Network environment
* Automation framework
* Profile configuration
* Browser mode

---

# WebRTC Testing With AI Browser Agents

AI browser agents add an additional automation layer.

A simplified architecture is:

```text id="y7h2p4"
AI Model
   ↓
AI Agent
   ↓
Automation Layer
   ↓
Browser Profile
   ↓
WebRTC + Network Environment
   ↓
Website
```

The AI model itself is not the WebRTC networking layer.

The underlying browser and network environment determine WebRTC behavior.

Therefore, testing an AI browser agent should include the actual browser profile, proxy, browser version, and network configuration.

See [AI Browser Agents](../ai-agents/ai-browser-agents.md) for the broader architecture.

---

# WebRTC Testing With MarketerBrowser

MarketerBrowser provides browser profiles and proxy-management capabilities that can be evaluated through controlled WebRTC testing.

A practical test process is:

1. Create a test profile.
2. Record the browser version.
3. Record the operating system.
4. Configure the test proxy if required.
5. Record the proxy type and location.
6. Run a WebRTC test.
7. Repeat the test several times.
8. Restart the browser.
9. Test again.
10. Compare another profile.
11. Change one configuration variable.
12. Repeat the experiment.

The purpose is to observe how the browser environment behaves under defined conditions.

You can learn more about MarketerBrowser at:

https://www.marketerbrowser.com/

---

# Example WebRTC Test Report

A simple report could look like this:

```text id="2b8k6m"
WebRTC Fingerprint Test

Date:
2026-09-04

Browser:
Chromium-based browser

Browser Version:
140.x

Operating System:
Windows

Profile:
Profile A

Proxy:
Residential proxy

IPv4:
Available

IPv6:
Available

Camera Permission:
Denied

Microphone Permission:
Denied

WebRTC Observation:

Run 1 → Result A
Run 2 → Result A
Run 3 → Result A
Run 4 → Result A
Run 5 → Result A

After Browser Restart:
Result A

Notes:
No configuration changes were made during the test.
```

This provides enough context for another researcher to reproduce the experiment.

---

# WebRTC Test Matrix

For larger tests, use a matrix.

| Test | Profile | Proxy   | IPv4 | IPv6 | WebRTC   |
| ---- | ------- | ------- | ---- | ---- | -------- |
| 1    | A       | None    | Yes  | No   | Result A |
| 2    | A       | Proxy A | Yes  | No   | Result B |
| 3    | B       | Proxy B | Yes  | Yes  | Result C |
| 4    | A       | Proxy A | Yes  | No   | Result B |

This makes relationships between network configuration and WebRTC observations easier to identify.

---

# Use Multiple WebRTC Test Sources

Different testing websites may use different WebRTC APIs and display different information.

A stronger methodology is:

```text id="p7k4d1"
WebRTC Test A
      ↓
WebRTC Test B
      ↓
WebRTC Test C
      ↓
Compare Observations
```

Do not assume that one website provides a complete view of WebRTC behavior.

---

# Save Screenshots and Test Results

For repeatable research, save the evidence.

A simple structure:

```text id="u4m9r1"
webrtc-test/
├── profile-a/
│   ├── run-01.png
│   ├── run-02.png
│   └── notes.txt
├── profile-b/
│   ├── run-01.png
│   ├── run-02.png
│   └── notes.txt
└── results.md
```

Record:

* Test date
* Browser version
* Operating system
* Profile
* Proxy
* IPv4/IPv6 environment
* Permission state
* WebRTC observation
* Test website
* Configuration changes

---

# Common WebRTC Testing Mistakes

## Mistake 1: Assuming the Proxy Controls Everything

A browser proxy does not automatically mean every WebRTC-related network characteristic will behave exactly like the proxy.

**Better:** test the actual browser environment.

---

## Mistake 2: Testing Only Once

A single result does not establish stability.

**Better:** repeat the same test several times.

---

## Mistake 3: Ignoring IPv6

An IPv6-enabled environment can behave differently from an IPv4-only environment.

**Better:** document the network environment.

---

## Mistake 4: Ignoring Permissions

Media permissions can affect what a website can observe.

**Better:** record camera and microphone permission states when relevant.

---

## Mistake 5: Changing Multiple Variables

Changing proxy, VPN, browser version, profile, and network simultaneously makes the result difficult to interpret.

**Better:** change one major variable at a time.

---

## Mistake 6: Treating WebRTC as the Complete Fingerprint

WebRTC is only one category of browser and network signal.

**Better:** evaluate it alongside Canvas, WebGL, fonts, audio, GPU, browser properties, and other relevant signals.

---

## Mistake 7: Treating a Test Result as a Guarantee

A WebRTC test represents an observation under specific conditions.

It cannot guarantee identical behavior on every website.

---

# What a Good WebRTC Test Should Answer

A useful experiment should answer questions such as:

### What information is exposed?

What WebRTC-related information can the test website observe?

### Is the result repeatable?

Does the same environment produce the same observation?

### Does the proxy affect the result?

Does changing the proxy correlate with a measurable change?

### Does the network environment matter?

Do IPv4, IPv6, VPN, or other network changes affect the result?

### Do browser profiles behave consistently?

Does each profile reproduce its expected environment?

### Does automation change the observation?

Does the automated browser behave differently from a manually launched browser?

These are measurable questions that produce useful technical evidence.

---

# WebRTC Testing Checklist

Before documenting a WebRTC experiment, verify:

* [ ] Browser version recorded
* [ ] Operating system recorded
* [ ] Profile identified
* [ ] Proxy configuration recorded
* [ ] IPv4/IPv6 environment documented
* [ ] Relevant permissions recorded
* [ ] Test website recorded
* [ ] Multiple test runs completed
* [ ] Browser restart tested
* [ ] Profile comparison performed where relevant
* [ ] Automation mode documented where applicable
* [ ] Screenshots or raw results saved
* [ ] Important configuration changes documented
* [ ] Results compared with other fingerprint signals
* [ ] Conclusions kept within the evidence

---

# Final Takeaway

WebRTC testing is useful because it examines a different part of the browser environment from graphics-oriented tests such as Canvas and WebGL.

A good WebRTC test should focus on observation and repeatability:

```text
Establish Baseline
        ↓
Record Network Environment
        ↓
Run WebRTC Test
        ↓
Repeat
        ↓
Test After Restart
        ↓
Compare Profiles
        ↓
Change One Variable
        ↓
Document Results
```

The most important lesson is simple:

**Do not assume what the browser exposes. Test it.**

A proxy, VPN, browser profile, browser version, operating system, permissions, and network configuration can all be relevant to the final environment.

WebRTC is one piece of the overall browser fingerprint and network picture. Testing it alongside [Canvas](../docs/canvas-fingerprint.md), [WebGL](../docs/webgl-fingerprint.md), [GPU](../docs/gpu-fingerprint.md), [Fonts](../docs/font-fingerprint.md), and other signals provides a much stronger understanding of the browser environment.
