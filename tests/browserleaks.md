# BrowserLeaks Browser Test: How to Audit Your Browser Fingerprint and Privacy Signals

Browser fingerprint testing is most useful when it gives you a structured view of the browser environment rather than a single score or identifier.

BrowserLeaks is one example of a public browser-testing resource that exposes different categories of browser and network information. It can be useful for learning what a website may be able to observe from a browser session.

This guide explains how to use browser testing sites such as BrowserLeaks as part of a structured browser-environment audit.

The goal is not to prove that a browser is "undetectable."

Instead, the goal is to answer practical questions:

* What information does the browser expose?
* Which signals are stable?
* Which signals change when the environment changes?
* Does a browser profile maintain the expected configuration?
* Does the proxy behave as expected?
* Are there unexpected network or browser signals?
* Can the results be reproduced?

For the broader methodology, see [Fingerprint Tests](./fingerprint-tests.md) and [Test Methodology](./test-methodology.md).

---

# What Is BrowserLeaks?

BrowserLeaks is a browser-testing website that provides tools for examining different browser and network characteristics.

The site contains multiple categories of tests rather than relying on one fingerprint mechanism.

Depending on the test, you may encounter information related to:

* IP addresses
* WebRTC
* Canvas
* WebGL
* Fonts
* JavaScript
* Screen characteristics
* Browser properties
* Network information
* Other browser-exposed signals

The exact tests and information available can change over time.

For this reason, treat BrowserLeaks as a testing resource rather than a permanent definition of every browser fingerprint signal.

---

# Why Use Browser Testing Sites?

A browser-testing site can provide a convenient way to inspect your current environment.

For example:

```text id="2aj9j8"
Browser
   ↓
Testing Website
   ↓
Browser-Exposed Signals
   ↓
Observed Results
```

This can be useful for:

* Browser configuration testing
* Privacy research
* Proxy testing
* Fingerprint research
* Profile testing
* Automation testing
* Cross-browser comparisons
* Troubleshooting unexpected browser behavior

The important part is how you interpret the results.

---

# BrowserLeaks Is Not a Single Fingerprint Test

One of the most important concepts is that a browser-testing website may expose many different categories of information.

A simplified model is:

```text id="x4f2j7"
Browser Test
    │
    ├── IP / Network
    ├── WebRTC
    ├── Canvas
    ├── WebGL
    ├── Fonts
    ├── Screen
    ├── JavaScript
    └── Browser Properties
```

These signals should not automatically be treated as one universal identifier.

Different websites may collect different combinations of signals.

Therefore, a result from one testing site should be interpreted in context.

---

# Start With a Clean Baseline

Before testing a configured browser profile, establish a baseline.

Record:

```text id="q8z2m4"
Browser:
Chromium-based browser

Version:
140.x

Operating System:
Windows

Profile:
Default

Proxy:
None

Date:
2026-09-04
```

Then visit the relevant testing pages.

Save the results.

This gives you a reference point.

---

# What Should You Test?

A browser environment audit can cover several categories.

## 1. IP and Network

Check what network-related information is visible to the testing website.

Record:

* Observed IP
* IP version
* Approximate location
* Network provider information when displayed
* Proxy or VPN configuration

Do not assume that a configured proxy automatically determines every network signal.

---

## 2. WebRTC

WebRTC can expose browser and network-related information depending on browser and network configuration.

Compare the observed WebRTC information with your expected environment.

For a dedicated methodology, see [WebRTC Fingerprint Test](./webrtc-test.md).

---

## 3. Canvas

Canvas tests examine browser graphics rendering behavior.

Record the result and repeat the test.

For more detail, see [Canvas Fingerprint Test](./canvas-test.md).

---

## 4. WebGL

WebGL testing can expose graphics-related information such as renderer and vendor characteristics.

Record:

* WebGL vendor
* WebGL renderer
* Relevant capabilities
* Test result

See [WebGL Fingerprint Test](./webgl-test.md).

---

## 5. Fonts

Font availability can contribute to browser fingerprinting.

A test may inspect which fonts appear to be available to web content.

Compare results across profiles or environments when relevant.

See [Font Fingerprinting](../docs/font-fingerprint.md).

---

## 6. Screen Characteristics

A browser can expose information about the display environment.

Depending on the test, this may include:

* Screen dimensions
* Available screen area
* Color depth
* Pixel depth
* Device-related screen properties

These values should be recorded when conducting profile comparisons.

---

## 7. JavaScript and Browser Properties

Testing sites may inspect browser-exposed JavaScript properties.

These can include information associated with:

* Browser capabilities
* Navigator properties
* Language settings
* Platform information
* Time zone
* Device characteristics

The exact properties available depend on the browser and website.

---

# Create a Test Record

Instead of simply taking a screenshot, create a structured record.

Example:

```text id="m4d8w2"
Browser Environment Audit

Date:
2026-09-04

Browser:
Chromium-based browser

Version:
140.x

Operating System:
Windows

Profile:
Profile A

Proxy:
Proxy A

IP:
Observed result

WebRTC:
Observed result

Canvas:
ABC123

WebGL:
Renderer A

Fonts:
Observed result

Screen:
1920 × 1080

Time Zone:
Observed result

Notes:
No configuration changes during test.
```

This turns a browser test into a reproducible experiment.

---

# Test the Same Profile Multiple Times

Repeatability is one of the most useful things you can measure.

Example:

```text id="v7r2m9"
Profile A

Run 1 → Result Set A
Run 2 → Result Set A
Run 3 → Result Set A
Run 4 → Result Set A
```

Now restart the browser.

```text id="w4k8x1"
After Restart

Run 1 → Result Set A
Run 2 → Result Set A
Run 3 → Result Set A
```

If the observations remain consistent, you have evidence that the environment is stable under those conditions.

---

# Compare Separate Browser Profiles

Profile testing is particularly useful when working with multiple isolated browser environments.

For example:

| Signal | Profile A  | Profile B  |
| ------ | ---------- | ---------- |
| Canvas | Result A   | Result B   |
| WebGL  | Renderer A | Renderer B |
| Fonts  | Set A      | Set B      |
| Screen | Config A   | Config B   |
| WebRTC | Result A   | Result B   |

Repeat the test to make sure the results are reproducible.

Do not assume that different values are automatically better.

The objective is to understand whether each profile behaves consistently according to its intended configuration.

For the underlying concept, see [Browser Profile Isolation](../docs/browser-profile-isolation.md).

---

# Test Proxy Configuration Separately

A useful browser audit should distinguish network-related changes from browser fingerprint changes.

Start with:

```text id="h7c1m3"
Profile A
Proxy: None
```

Record the results.

Then configure:

```text id="z2m5q9"
Profile A
Proxy: Proxy A
```

Run the same tests.

Now compare:

```text id="q6n4x8"
Network Signals
→ May Change

Canvas
→ May Remain the Same

WebGL
→ May Remain the Same

Browser Properties
→ May Remain the Same
```

The exact results depend on the browser and environment.

The important lesson is that **network identity and browser identity are different categories**.

See [Proxy and Browser Fingerprint](../proxy/proxy-and-browser-fingerprint.md).

---

# Check Geographic Consistency

Location-related signals can come from multiple sources.

Depending on the website and browser environment, relevant information may include:

* IP-based location
* Browser time zone
* Language
* Locale
* Geolocation permissions
* Other browser-exposed settings

These signals do not necessarily have to be identical in every legitimate scenario, but unexpected combinations are worth investigating.

For example:

```text id="1f6p9a"
Observed IP Location:
Country A

Browser Time Zone:
Region associated with Country B
```

This does not automatically mean that the browser has a problem.

It means the environment contains signals that should be understood.

See [Proxy Geolocation](../proxy/proxy-geolocation.md).

---

# BrowserLeaks and Fingerprint Consistency

One of the most useful questions is not:

> "How unique is my browser?"

Instead:

> "Is my browser environment consistent with its intended configuration?"

For example:

```text id="4r8x2j"
Profile A

Canvas      → Stable
WebGL       → Stable
Fonts       → Stable
Screen      → Stable
WebRTC      → Stable
Network     → Expected
```

This gives you a much more practical picture of the browser environment.

---

# Test Browser Updates

A browser update can affect fingerprint-related behavior.

Before an update:

```text id="7m1k5d"
Browser 140
Canvas → A
WebGL → B
Browser Properties → C
```

After an update:

```text id="p2c8w4"
Browser 141
Canvas → A
WebGL → D
Browser Properties → E
```

Record the differences.

This is especially important for long-running browser-profile environments.

A fingerprint test should always record the browser version.

---

# Test Operating System Changes

Operating systems can influence browser behavior.

For example:

```text id="5k9q2v"
Windows → Result Set A
macOS   → Result Set B
Linux   → Result Set C
```

If you are testing operating-system differences, keep the browser version and other major variables as consistent as possible.

This creates a more meaningful comparison.

---

# Test Headed and Headless Browsers

Automated browser environments can behave differently depending on how they are launched.

A controlled experiment might compare:

```text id="8c3m7v"
Headed Browser
→ Result Set A

Headless Browser
→ Result Set B
```

If differences appear, record the browser version, automation framework, launch configuration, and profile.

Do not attribute every difference to headless mode without further testing.

---

# BrowserLeaks and Automation

Browser testing can be useful when evaluating automated browser environments.

For example, compare:

```text id="n5j2c7"
Manual Browser
      ↓
Test Website
      ↓
Result Set A
```

against:

```text id="t8q4m1"
Automated Browser
      ↓
Test Website
      ↓
Result Set B
```

Then investigate the variables.

Possible differences may come from:

* Browser launch options
* Browser version
* Profile configuration
* Headed/headless mode
* Operating system
* Graphics environment
* Automation framework

See [Browser Automation](../automation/browser-automation.md).

---

# BrowserLeaks and AI Browser Agents

AI browser agents add another layer to the browser environment.

A simplified architecture is:

```text id="y5m8r3"
AI Model
   ↓
AI Agent
   ↓
Automation Layer
   ↓
Browser Profile
   ↓
Browser + Network Environment
   ↓
Testing Website
```

When testing an AI browser agent, evaluate the actual browser environment.

The AI model does not itself determine the browser's Canvas, WebGL, WebRTC, or network characteristics.

Those are properties of the browser and its surrounding environment.

For more information, see [AI Browser Agents](../ai-agents/ai-browser-agents.md).

---

# Using BrowserLeaks With MarketerBrowser

MarketerBrowser can be evaluated using the same browser-audit methodology.

A practical workflow is:

1. Create a test profile.
2. Record the browser version.
3. Record the operating system.
4. Configure the proxy if required.
5. Run the relevant browser tests.
6. Save the results.
7. Repeat the tests.
8. Restart the browser.
9. Test again.
10. Create another profile.
11. Compare the observations.
12. Change one variable.
13. Repeat the experiment.

This approach produces measurable observations rather than relying on generalized claims.

You can learn more about MarketerBrowser at:

https://www.marketerbrowser.com/

---

# Example Multi-Profile Audit

Suppose you have three test profiles.

```text id="c2v7m9"
Profile A
Proxy: A

Profile B
Proxy: B

Profile C
Proxy: C
```

Run the same test suite.

| Signal | Profile A | Profile B | Profile C |
| ------ | --------- | --------- | --------- |
| IP     | A         | B         | C         |
| Canvas | A         | B         | C         |
| WebGL  | A         | B         | C         |
| Fonts  | A         | B         | C         |
| Screen | A         | B         | C         |
| WebRTC | A         | B         | C         |

Then repeat the entire test.

The goal is to determine:

* Which signals remain stable
* Which signals change
* Which signals are affected by the proxy
* Which signals are profile-specific
* Which results appear unexpected

This is far more informative than simply asking whether the browser "passes" a fingerprint test.

---

# Build a Test Matrix

For larger evaluations, maintain a test matrix.

| Test | Browser | Profile | Proxy   | Canvas | WebGL | WebRTC |
| ---- | ------- | ------- | ------- | ------ | ----- | ------ |
| 1    | 140     | A       | None    | A      | A     | A      |
| 2    | 140     | A       | Proxy A | A      | A     | B      |
| 3    | 140     | B       | Proxy B | B      | B     | C      |
| 4    | 141     | A       | Proxy A | A      | C     | B      |

This allows you to identify patterns.

For example, if only the WebGL result changes after a browser update, that becomes a specific observation worth investigating.

---

# Save Evidence

For serious testing, save:

* Screenshots
* Test URLs
* Browser version
* Operating system
* Profile
* Proxy configuration
* Date and time
* Test results
* Configuration changes
* Notes

A simple directory might look like:

```text id="9p4x6m"
browser-audit/
├── profile-a/
│   ├── network.png
│   ├── webrtc.png
│   ├── canvas.png
│   ├── webgl.png
│   └── notes.md
├── profile-b/
│   ├── network.png
│   ├── webrtc.png
│   ├── canvas.png
│   ├── webgl.png
│   └── notes.md
└── results.md
```

This creates an evidence trail.

---

# Compare Before and After Changes

A useful audit compares controlled states.

For example:

```text id="0k7n4x"
Before:

Browser 140
Profile A
Proxy A

Canvas → A
WebGL → B
WebRTC → C
```

After changing only the proxy:

```text id="8q2m5r"
After:

Browser 140
Profile A
Proxy B

Canvas → A
WebGL → B
WebRTC → D
```

Now you can investigate which observations appear network-dependent.

This is much more useful than making several changes simultaneously.

---

# Common BrowserLeaks Testing Mistakes

## Mistake 1: Treating One Test Page as the Entire Internet

Different websites collect different information.

**Better:** use multiple test sources when possible.

---

## Mistake 2: Focusing Only on a Score

A fingerprint score is a summary produced by a particular test.

**Better:** examine the underlying signals.

---

## Mistake 3: Testing Only Once

One result cannot establish stability.

**Better:** repeat the test.

---

## Mistake 4: Ignoring Browser Version

Browser updates can affect observable behavior.

**Better:** record the exact version.

---

## Mistake 5: Changing Multiple Variables

Changing the proxy, browser, profile, and operating system simultaneously makes results difficult to interpret.

**Better:** change one major variable at a time.

---

## Mistake 6: Confusing Proxy Identity With Browser Identity

A proxy changes network routing, not necessarily every browser fingerprint signal.

**Better:** test network and browser signals separately.

---

## Mistake 7: Assuming Different Means Better

A different Canvas or WebGL result is not automatically evidence of improved privacy.

**Better:** evaluate consistency and context.

---

## Mistake 8: Treating Test Results as Guarantees

A browser test measures observable behavior under specific conditions.

It cannot guarantee how every website will evaluate the browser.

---

# How to Interpret an Unexpected Result

Suppose a test suddenly reports a different WebGL renderer.

Do not immediately change the entire browser configuration.

Instead:

### Step 1: Repeat the test

```text id="p3m7x8"
Run 1 → Renderer B
Run 2 → Renderer B
Run 3 → Renderer B
```

### Step 2: Check the browser version

Did the browser update?

### Step 3: Check the profile

Are you testing the same profile?

### Step 4: Check the graphics environment

Did the device or GPU configuration change?

### Step 5: Check the test source

Does another testing website show the same result?

### Step 6: Document the observation

Record the change instead of hiding it.

This produces a much stronger technical investigation.

---

# A Practical Browser Audit Workflow

Use this workflow for a repeatable browser environment audit:

```text id="j8c4p1"
1. Define the objective
        ↓
2. Record browser environment
        ↓
3. Establish baseline
        ↓
4. Run network tests
        ↓
5. Run fingerprint tests
        ↓
6. Save evidence
        ↓
7. Repeat
        ↓
8. Restart browser
        ↓
9. Repeat again
        ↓
10. Compare profiles
        ↓
11. Change one variable
        ↓
12. Repeat experiment
        ↓
13. Document conclusions
```

---

# Browser Audit Checklist

Before considering an audit complete:

* [ ] Browser version recorded
* [ ] Operating system recorded
* [ ] Profile identified
* [ ] Proxy configuration recorded
* [ ] Network environment documented
* [ ] IP information checked
* [ ] WebRTC tested
* [ ] Canvas tested
* [ ] WebGL tested
* [ ] Fonts tested
* [ ] Screen characteristics recorded
* [ ] Browser properties reviewed
* [ ] Multiple runs completed
* [ ] Browser restart tested
* [ ] Separate profiles compared
* [ ] Browser updates considered
* [ ] Automation environment documented where applicable
* [ ] Screenshots saved
* [ ] Results interpreted conservatively

---

# What Browser Testing Can and Cannot Tell You

## Browser testing can help you understand:

* What information a browser exposes
* Whether a configuration is stable
* How profiles differ
* How proxies affect observed network signals
* How browser updates affect results
* How automation environments compare
* Which browser signals require further investigation

## Browser testing cannot prove:

* Complete anonymity
* Complete privacy
* Guaranteed detection avoidance
* Guaranteed CAPTCHA avoidance
* That one browser configuration works identically on every website
* That a particular fingerprint is permanently unique

Testing is evidence, not a guarantee.

---

# Final Takeaway

BrowserLeaks and similar testing resources are valuable because they let you inspect the browser environment from the perspective of web-accessible signals.

The best way to use them is as part of a controlled testing process:

```text id="6v3p9a"
Baseline
   ↓
Measure
   ↓
Repeat
   ↓
Compare
   ↓
Change One Variable
   ↓
Measure Again
   ↓
Document
```

Do not reduce browser fingerprint testing to a single score.

Look at the individual signals, understand how they relate to the browser environment, and record the conditions under which each result was obtained.

That approach turns a browser-testing website into a useful research tool for evaluating browser profiles, proxies, automation environments, and fingerprint configurations.

For deeper testing, continue with:

* [Fingerprint Tests](./fingerprint-tests.md)
* [Test Methodology](./test-methodology.md)
* [Canvas Fingerprint Test](./canvas-test.md)
* [WebGL Fingerprint Test](./webgl-test.md)
* [WebRTC Fingerprint Test](./webrtc-test.md)
