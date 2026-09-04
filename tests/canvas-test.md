# Canvas Fingerprint Test: How to Measure and Compare Browser Canvas Fingerprints

Canvas fingerprinting is one of the most commonly discussed browser fingerprint signals. It is useful for understanding how a browser environment renders graphics and how consistently that rendering can be observed across sessions, profiles, devices, and browser configurations.

This guide explains how to test Canvas fingerprint behavior systematically.

The goal is not to prove that a browser is "undetectable." A good Canvas test should instead answer practical questions:

* Does the browser produce a stable Canvas result?
* Does the result change when the environment changes?
* Do separate browser profiles remain isolated?
* Does changing the browser, operating system, or graphics environment affect the result?
* Does a fingerprint configuration remain consistent over repeated tests?

For a broader introduction to fingerprint testing, see [Fingerprint Tests](./fingerprint-tests.md).

---

## What Is a Canvas Fingerprint?

The HTML5 Canvas API allows websites to render graphics, text, shapes, gradients, and other visual elements inside the browser.

A website can render a specific Canvas test and examine the resulting output.

Small differences in rendering can occur because of differences in:

* Operating system
* Browser implementation
* Graphics hardware
* GPU drivers
* Font rendering
* Browser settings
* Graphics libraries
* Browser fingerprint configuration

Those differences can contribute to a broader browser fingerprint.

Canvas fingerprinting should therefore be treated as **one signal among many**, rather than a complete identification mechanism by itself.

---

## Why Test Canvas Fingerprints?

Canvas testing is useful for several different reasons.

### 1. Browser fingerprint research

Researchers can use Canvas tests to understand how browser environments differ.

### 2. Profile testing

If you operate multiple isolated browser profiles, testing can help verify whether profiles behave as expected.

### 3. Browser configuration testing

Changing browser versions, operating systems, graphics environments, or fingerprint settings may affect Canvas output.

Testing makes those changes measurable.

### 4. Anti-detect browser evaluation

When evaluating an anti-detect browser, Canvas testing can help answer practical questions about its fingerprint management.

Instead of asking:

> "Is this browser undetectable?"

A better question is:

> "How does its Canvas fingerprint behave under controlled testing?"

That produces a much more useful result.

---

# How a Canvas Fingerprint Test Works

A typical Canvas test follows a simple process:

```text
Browser
   ↓
Canvas Rendering
   ↓
Rendered Image / Pixel Data
   ↓
Fingerprint Calculation
   ↓
Result
```

The test page renders a predefined Canvas scene.

The resulting pixels can then be processed into a value or signature that makes comparison easier.

For example:

```text
Test Run 1 → Canvas Result A
Test Run 2 → Canvas Result A
Test Run 3 → Canvas Result A
```

This suggests that the environment is producing a stable result under those conditions.

If the results are:

```text
Test Run 1 → Canvas Result A
Test Run 2 → Canvas Result B
Test Run 3 → Canvas Result C
```

then something in the testing environment may be changing.

That does not automatically mean the browser is malfunctioning. The important next step is identifying what changed.

---

# What Should You Record?

A useful Canvas experiment should record more than the fingerprint result.

At minimum, record:

| Variable         | Example                  |
| ---------------- | ------------------------ |
| Date             | 2026-09-04               |
| Browser          | Chromium-based browser   |
| Browser version  | Version number           |
| Operating system | Windows                  |
| Profile          | Profile A                |
| Proxy            | Proxy configuration      |
| Canvas result    | Test result              |
| Test website     | Test page used           |
| Test run         | Run 1                    |
| Notes            | No configuration changes |

For more detailed experiments, also record:

* Screen resolution
* Device type
* GPU information
* Browser engine
* User-agent configuration
* WebGL configuration
* Font configuration
* Proxy location
* Profile configuration
* Whether automation was enabled
* Whether the browser was running headed or headless

This makes your results reproducible.

---

# Establish a Baseline First

Never start a fingerprint experiment by changing five settings at once.

Start with a baseline.

For example:

```text
Browser: Chromium
Version: X
OS: Windows
Profile: Default
Proxy: None

Canvas Result:
ABC123
```

Run the same test several times.

```text
Run 1 → ABC123
Run 2 → ABC123
Run 3 → ABC123
Run 4 → ABC123
```

Now you have a baseline.

Only after establishing the baseline should you change one variable.

---

# Change One Variable at a Time

This is one of the most important principles in fingerprint testing.

Suppose you change:

* Browser version
* Proxy
* Screen resolution
* GPU settings
* Canvas settings

all at once.

If the Canvas result changes, you do not know why.

Instead, use controlled experiments.

### Experiment A

Keep everything unchanged.

```text
Browser: Version X
OS: Windows
Profile: A
Proxy: None

Canvas: ABC123
```

### Experiment B

Change only the browser version.

```text
Browser: Version Y
OS: Windows
Profile: A
Proxy: None

Canvas: DEF456
```

Now you have evidence that the browser-version change may be relevant.

This does not prove causation by itself, but it gives you a much stronger basis for further testing.

---

# Repeatability Matters

One Canvas result is not enough.

A proper test should be repeated.

For example:

```text
Profile A

Run 1 → ABC123
Run 2 → ABC123
Run 3 → ABC123
Run 4 → ABC123
Run 5 → ABC123
```

This indicates strong repeatability under the same conditions.

Now test again after restarting the browser.

```text
Before Restart

ABC123
ABC123
ABC123

After Restart

ABC123
ABC123
ABC123
```

If the result remains consistent, that is useful evidence of stability.

---

# Testing Multiple Profiles

Profile isolation is particularly important when testing multi-account browser environments.

Create two separate profiles:

```text
Profile A
Profile B
```

Test each several times.

Example:

| Profile | Run 1  | Run 2  | Run 3  |
| ------- | ------ | ------ | ------ |
| A       | ABC123 | ABC123 | ABC123 |
| B       | XYZ789 | XYZ789 | XYZ789 |

This tells you that the two profiles produce different Canvas results while remaining stable individually.

However, different fingerprints are not automatically better.

The purpose of profile testing is to understand **isolation and consistency**, not simply to maximize uniqueness.

Learn more about the broader concept in [Browser Profile Isolation](../docs/browser-profile-isolation.md).

---

# Testing the Same Profile Over Time

Longitudinal testing can be even more useful than a single experiment.

For example:

```text
Day 1 → ABC123
Day 2 → ABC123
Day 3 → ABC123
Day 7 → ABC123
Day 14 → ABC123
```

This provides evidence about stability over time.

If the result changes:

```text
Day 1 → ABC123
Day 2 → ABC123
Day 3 → DEF456
```

investigate what changed around Day 3.

Possible factors include:

* Browser update
* Operating system update
* Profile configuration change
* Graphics driver change
* Browser configuration change
* Different device
* Different testing environment

Do not immediately conclude that the Canvas system itself is unreliable.

---

# Canvas and Browser Updates

Browser updates can change rendering behavior.

When evaluating a browser environment, record the browser version.

For example:

```text
Browser Version: 140.x
Canvas: ABC123
```

After updating:

```text
Browser Version: 141.x
Canvas: DEF456
```

That change is worth documenting.

This is one reason fingerprint testing should include browser-version information.

A fingerprint result without environment information is difficult to interpret.

---

# Canvas and GPU Environment

Canvas rendering can be influenced by the graphics environment.

Depending on the browser and operating system, relevant factors may include:

* GPU
* GPU driver
* Graphics libraries
* Browser graphics implementation
* Hardware acceleration
* Operating system rendering behavior

This is why Canvas should not be tested completely independently from the rest of the browser environment.

For related testing, see:

* [WebGL Fingerprint](../docs/webgl-fingerprint.md)
* [GPU Fingerprint](../docs/gpu-fingerprint.md)

---

# Canvas and Fonts

Text rendering is often part of Canvas tests.

That means font availability and rendering can matter.

For example, a test may render:

```text
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz
0123456789
```

Small rendering differences can affect the final pixel output.

Therefore, when comparing Canvas results, document significant font-environment differences.

See [Font Fingerprinting](../docs/font-fingerprint.md) for more information.

---

# Canvas and Operating System

The same browser application can behave differently across operating systems.

For example:

```text
Windows + Chromium → Canvas A
macOS + Chromium   → Canvas B
Linux + Chromium   → Canvas C
```

This does not mean that every browser on each operating system will produce one universal result.

The point is that the complete rendering environment matters.

When conducting comparisons, keep the operating system documented.

---

# Canvas and Proxy Testing

A proxy primarily changes network routing and IP-related characteristics.

It should not be assumed that changing a proxy automatically changes a Canvas fingerprint.

For example:

```text
Profile A
Canvas: ABC123

Proxy 1
Canvas: ABC123

Proxy 2
Canvas: ABC123
```

That can be perfectly reasonable.

The network identity and browser rendering identity are different parts of the environment.

For broader testing, see [Proxy and Browser Fingerprint](../proxy/proxy-and-browser-fingerprint.md).

---

# Canvas and Browser Profiles

A browser profile can contain its own configuration, cookies, local storage, browser settings, and fingerprint-related parameters depending on the browser software.

When evaluating profile isolation, test each profile independently.

Example:

```text
Profile A
Canvas → ABC123

Profile B
Canvas → XYZ789

Profile C
Canvas → LMN456
```

Then repeat:

```text
Profile A
Canvas → ABC123

Profile B
Canvas → XYZ789

Profile C
Canvas → LMN456
```

The important observation is whether each profile behaves consistently according to its configuration.

---

# Testing With MarketerBrowser

MarketerBrowser provides browser profiles and fingerprint-management capabilities that can be evaluated using the same controlled methodology.

For a meaningful test:

1. Create a test profile.
2. Record its browser environment.
3. Run a Canvas fingerprint test.
4. Repeat the test several times.
5. Restart the browser.
6. Test again.
7. Create another profile.
8. Compare the results.
9. Change one configuration variable.
10. Repeat the experiment.

The goal should be to measure actual behavior rather than rely on a general claim about fingerprint protection.

You can learn more about MarketerBrowser at:

https://www.marketerbrowser.com/

---

# A Simple Canvas Test Matrix

A small test matrix can make results much easier to understand.

| Test | Browser   | Profile | Proxy | Canvas |
| ---- | --------- | ------- | ----- | ------ |
| 1    | Version A | A       | None  | ABC123 |
| 2    | Version A | A       | None  | ABC123 |
| 3    | Version A | B       | None  | XYZ789 |
| 4    | Version A | B       | None  | XYZ789 |
| 5    | Version B | A       | None  | DEF456 |

This allows you to see patterns immediately.

You can expand the matrix when testing more variables.

---

# Testing Canvas Stability vs. Randomness

A common mistake is assuming that a changing fingerprint is automatically desirable.

That is too simplistic.

Consider two environments.

### Environment A

```text
Run 1 → ABC123
Run 2 → ABC123
Run 3 → ABC123
Run 4 → ABC123
```

### Environment B

```text
Run 1 → ABC123
Run 2 → DEF456
Run 3 → XYZ789
Run 4 → LMN456
```

Environment B is more variable, but that does not automatically make it a better browser environment.

For many real-world workflows, consistency is an important property.

The correct question is:

> Does the browser produce the expected and appropriately consistent environment for the use case?

---

# Use Multiple Test Sources

Do not rely on a single fingerprint-testing website.

Different test sites may:

* Use different Canvas tests
* Process results differently
* Display different information
* Combine Canvas with other signals
* Update their testing methods

A stronger methodology is:

```text
Test Site A
      ↓
Test Site B
      ↓
Test Site C
      ↓
Compare Observations
```

If several independent tests show similar behavior, your conclusion becomes more useful.

---

# Keep Screenshots and Raw Results

When conducting serious testing, save evidence.

Useful evidence includes:

* Screenshot of the test result
* Browser version
* Operating system
* Profile name
* Test date
* Proxy configuration
* Canvas result
* Relevant browser settings

A simple folder structure could be:

```text
canvas-test/
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

This makes future comparisons much easier.

---

# Example Test Report

A concise report might look like this:

```text
Canvas Fingerprint Test

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

Test Site:
Canvas Test A

Results:

Run 1 → ABC123
Run 2 → ABC123
Run 3 → ABC123
Run 4 → ABC123
Run 5 → ABC123

Browser Restart:
Stable

Notes:
No browser configuration changes were made during the test.
```

This is much more valuable than simply writing:

```text
Canvas fingerprint works.
```

---

# Common Canvas Testing Mistakes

## Mistake 1: Testing Only Once

One result does not establish stability.

**Better:** perform multiple runs.

---

## Mistake 2: Changing Multiple Variables

If you change browser version, proxy, profile, and operating system simultaneously, you cannot identify the cause of a change.

**Better:** change one major variable at a time.

---

## Mistake 3: Ignoring Browser Version

Browser updates can affect rendering behavior.

**Better:** record the exact browser version.

---

## Mistake 4: Treating Canvas as the Entire Fingerprint

Canvas is only one browser signal.

Other signals can include:

* WebGL
* Audio
* Fonts
* WebRTC
* GPU
* Screen characteristics
* Browser properties
* Network information
* Cookies and session state

See [Browser Fingerprinting](../docs/browser-fingerprinting.md) for the broader picture.

---

## Mistake 5: Assuming a Different Result Is Automatically Better

Fingerprint testing is not a competition to generate as many different values as possible.

The objective is controlled observation.

---

## Mistake 6: Confusing IP Changes With Canvas Changes

A proxy changes network characteristics.

It does not automatically mean the browser's Canvas rendering should change.

---

# What a Good Canvas Test Should Answer

At the end of an experiment, you should be able to answer questions such as:

### Is the result repeatable?

Can the same environment reproduce the same result?

### Is the result affected by browser updates?

Does changing the browser version produce a measurable difference?

### Are profiles isolated?

Do separate profiles behave independently?

### Does the result remain stable after restarting?

Does the profile reproduce the same Canvas behavior?

### Which variables appear relevant?

Can you identify environmental changes associated with different results?

These are meaningful testing questions.

---

# Canvas Testing for Automated Browsers

Canvas behavior can also be evaluated when browsers are controlled by automation frameworks.

Examples include:

* Playwright
* Puppeteer
* Selenium

The important point is to distinguish the browser environment from the automation framework.

A useful experiment might compare:

```text
Manual Browser
      ↓
Canvas Result A

Automated Browser
      ↓
Canvas Result B
```

If the results differ, investigate the environment rather than immediately assuming that automation itself caused the difference.

Relevant factors may include:

* Browser launch parameters
* Headed vs. headless mode
* Browser version
* Profile configuration
* Operating system
* Graphics environment
* Automation configuration

See [Browser Automation](../automation/browser-automation.md) for broader automation concepts.

---

# Canvas Testing and AI Browser Agents

AI browser agents introduce another layer to the testing environment.

A simplified architecture looks like:

```text
AI Model
   ↓
AI Agent
   ↓
Browser Automation
   ↓
Browser Profile
   ↓
Canvas + Other Fingerprint Signals
   ↓
Website
```

The AI model does not directly create a Canvas fingerprint.

The browser environment does.

Therefore, when testing AI browser workflows, document the actual browser environment used by the agent.

---

# Interpreting Results Carefully

A Canvas test result should not be interpreted as proof of:

* Complete anonymity
* Complete browser privacy
* Guaranteed detection avoidance
* Guaranteed CAPTCHA avoidance
* Unique identity
* Permanent fingerprint stability

A Canvas result is simply evidence about one aspect of a browser environment under specific test conditions.

The strongest conclusions are narrow and measurable.

For example:

> "The same profile produced the same Canvas result across five repeated tests after a browser restart."

That is a useful technical observation.

By comparison:

> "This browser cannot be detected."

That is not a conclusion that a Canvas test can establish.

---

# Recommended Canvas Testing Workflow

Use this process when evaluating a browser or browser-profile system:

```text
1. Define the test objective
        ↓
2. Record the baseline environment
        ↓
3. Run the Canvas test
        ↓
4. Repeat several times
        ↓
5. Restart the browser
        ↓
6. Repeat the test
        ↓
7. Test another profile
        ↓
8. Change one variable
        ↓
9. Repeat the experiment
        ↓
10. Document the results
```

This produces much stronger evidence than a single fingerprint screenshot.

---

# Canvas Testing Checklist

Before publishing or relying on a Canvas test, verify:

* [ ] Browser version recorded
* [ ] Operating system recorded
* [ ] Profile identified
* [ ] Proxy configuration documented
* [ ] Test website recorded
* [ ] Multiple test runs completed
* [ ] Browser restart tested
* [ ] Profile comparison completed where relevant
* [ ] Important configuration changes documented
* [ ] Screenshots or raw results saved
* [ ] Results interpreted conservatively
* [ ] Other fingerprint signals considered

---

# Final Takeaway

Canvas fingerprint testing is most useful when treated as an experiment rather than a marketing claim.

A reliable test should establish a baseline, repeat measurements, control variables, record the browser environment, and document changes.

The key principles are simple:

```text
Measure
Repeat
Control Variables
Document
Compare
Interpret Carefully
```

Canvas is only one part of browser fingerprinting, but it is a useful signal for understanding how browser environments behave.

For a broader testing framework, continue with [Fingerprint Tests](./fingerprint-tests.md) and [Test Methodology](./test-methodology.md).
