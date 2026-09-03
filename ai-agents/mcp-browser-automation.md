# MCP Browser Automation: How AI Agents Control Web Browsers

The way AI interacts with software is changing.

Instead of using an AI model only to generate text, modern AI agents can interact with external tools. They can search information, work with files, call APIs, and in some cases control web browsers.

One technology that can help connect AI models with external tools is **MCP — Model Context Protocol**.

When MCP is combined with browser automation, an AI agent can potentially interact with websites through structured browser tools.

This creates a new architecture:

```text id="mcp001"
AI Model
    ↓
AI Agent
    ↓
MCP
    ↓
Browser Tools
    ↓
Browser Automation
    ↓
Browser
    ↓
Website
```

This guide explains MCP browser automation, how the architecture works, how MCP relates to Playwright, Puppeteer, Selenium, browser profiles, fingerprints, proxies, and AI agents, and what developers should consider when building MCP-powered browser workflows.

---

# What Is MCP?

MCP stands for **Model Context Protocol**.

At a high level, MCP provides a standardized way for AI applications to interact with external tools and resources.

Instead of building a completely custom integration for every AI application, an MCP-based architecture can expose capabilities through a structured tool interface.

Conceptually:

```text id="mcp002"
AI Application
      ↓
    MCP
      ↓
External Tools
```

Those tools can provide capabilities such as:

* Browser control
* File access
* Database operations
* Search
* APIs
* Development tools
* Other application-specific functions

The exact capabilities depend on the MCP server and implementation.

---

# What Is MCP Browser Automation?

MCP browser automation means exposing browser-control functionality to an AI system through MCP.

A simplified architecture is:

```text id="mcp003"
AI Model
    ↓
AI Agent
    ↓
MCP Client
    ↓
MCP Browser Server
    ↓
Browser Automation Framework
    ↓
Browser
```

The AI agent can then interact with browser tools instead of directly manipulating the browser implementation.

For example, an MCP browser tool might conceptually expose operations such as:

```text id="mcp004"
navigate()
click()
type()
scroll()
read_page()
screenshot()
```

The actual tool names and parameters depend on the implementation.

---

# Why MCP Matters for Browser Automation

Traditional browser automation often requires developers to write explicit code.

For example:

```text id="mcp005"
Developer
    ↓
Automation Script
    ↓
Browser
    ↓
Website
```

With an AI agent, the architecture can become:

```text id="mcp006"
Developer
    ↓
AI Agent
    ↓
MCP
    ↓
Browser Tools
    ↓
Browser
```

The developer defines the available capabilities.

The AI agent can then reason about which capabilities to use.

This can make browser automation more flexible for workflows where the exact sequence of actions is not always known in advance.

---

# MCP Client vs MCP Server

MCP architectures commonly involve two important components.

## MCP Client

The client is the component that connects an AI application to MCP servers.

Conceptually:

```text id="mcp007"
AI Application
      ↓
MCP Client
      ↓
MCP Server
```

## MCP Server

The MCP server exposes tools or resources.

For browser automation:

```text id="mcp008"
MCP Server
 ├── Navigate
 ├── Click
 ├── Type
 ├── Read
 └── Screenshot
```

The exact implementation depends on the MCP server.

---

# Browser Automation Through MCP

A complete browser workflow might look like:

```text id="mcp009"
User
 ↓
AI Agent
 ↓
MCP Tool
 ↓
Browser Automation
 ↓
Browser
 ↓
Website
```

Suppose the user asks an agent to research information from several web pages.

The agent could conceptually:

```text id="mcp010"
Understand request
       ↓
Open search page
       ↓
Read results
       ↓
Open relevant pages
       ↓
Extract information
       ↓
Compare results
       ↓
Return summary
```

The browser actions are performed by tools rather than by the language model itself.

---

# MCP Does Not Replace the Browser

MCP is a communication and tool-interface layer.

It does not inherently replace:

* Chromium
* Firefox
* Playwright
* Puppeteer
* Selenium
* Browser profiles
* Proxy systems

Instead, it can connect an AI system to those technologies.

A useful architecture is:

```text id="mcp011"
AI Agent
    ↓
MCP
    ↓
Automation Framework
    ↓
Browser
```

MCP sits above the browser automation implementation.

---

# MCP + Playwright

Playwright can serve as the browser automation layer underneath an MCP interface.

Conceptually:

```text id="mcp012"
AI Agent
    ↓
MCP
    ↓
Playwright
    ↓
Chromium / Browser
    ↓
Website
```

Playwright handles browser operations.

MCP exposes those operations to the AI system.

The AI agent determines which actions are appropriate.

See:

[Playwright Automation](../automation/playwright.md)

---

# MCP + Puppeteer

Puppeteer can also be used as a browser automation layer.

A conceptual architecture is:

```text id="mcp013"
AI Agent
    ↓
MCP
    ↓
Puppeteer
    ↓
Chromium
    ↓
Website
```

Puppeteer handles browser control while the MCP layer can expose selected capabilities to the AI agent.

See:

[Puppeteer Automation](../automation/puppeteer.md)

---

# MCP + Selenium

Selenium can similarly sit below an MCP browser interface.

```text id="mcp014"
AI Agent
    ↓
MCP
    ↓
Selenium
    ↓
WebDriver
    ↓
Browser
```

This can be particularly relevant to organizations that already have Selenium-based testing infrastructure.

See:

[Selenium Automation](../automation/selenium.md)

---

# MCP Browser Tools

An MCP browser server might expose a collection of tools.

For example:

```text id="mcp015"
Browser Tools

navigate
click
type
scroll
go_back
reload
read_page
get_url
screenshot
```

A more advanced implementation could expose additional capabilities.

The important design principle is **least privilege**.

An AI agent should receive only the browser capabilities it actually needs.

---

# Tool Design Matters

A poorly designed browser tool can make an AI agent difficult to control.

For example, a tool with a huge number of unrelated parameters can be difficult for an agent to use reliably.

Smaller, clearly defined operations can be easier to reason about:

```text id="mcp016"
navigate(url)

click(element)

type(element, text)

screenshot()

read_page()
```

The exact API is implementation-specific.

Good tool design should emphasize:

* Clear descriptions
* Predictable parameters
* Useful error messages
* Appropriate permissions
* Safe defaults

---

# MCP and the AI Agent Loop

MCP fits naturally into the AI browser-agent loop.

```text id="mcp017"
Observe
   ↓
Reason
   ↓
Choose Tool
   ↓
MCP
   ↓
Execute
   ↓
Observe Result
   ↓
Reason Again
```

For example:

```text id="mcp018"
Agent sees login page
       ↓
Chooses click tool
       ↓
MCP executes click
       ↓
Browser changes page
       ↓
Agent observes result
       ↓
Chooses next action
```

This feedback loop is central to adaptive browser automation.

---

# MCP and Browser Profiles

A browser profile provides a persistent browser environment.

Depending on the browser system, it may contain:

* Cookies
* Local storage
* Session state
* Browser settings
* Authentication state
* Fingerprint configuration

MCP can potentially expose profile-management operations to an AI agent.

For example:

```text id="mcp019"
AI Agent
    ↓
MCP
    ↓
Profile Manager
    ├── list_profiles()
    ├── open_profile()
    ├── close_profile()
    └── profile_status()
```

The exact implementation depends on the browser platform.

---

# Why Profile Isolation Matters

Consider an AI system managing several independent workflows.

Without isolation:

```text id="mcp020"
AI Agent
    ↓
Shared Browser
    ↓
Shared Cookies
    ↓
Shared Session
```

With isolated profiles:

```text id="mcp021"
AI Agent
    ├── Profile A
    ├── Profile B
    ├── Profile C
    └── Profile D
```

Each workflow can have its own browser state.

This is useful for:

* QA
* Research
* E-commerce
* Localization testing
* Multi-environment testing
* Administrative workflows

See:

[Browser Profile Isolation](../docs/browser-profile-isolation.md)

---

# MCP and Browser Fingerprints

A browser controlled through MCP is still a browser.

Websites can potentially observe browser characteristics such as:

* Browser version
* Operating system
* Screen properties
* Canvas
* WebGL
* Audio
* Fonts
* WebRTC
* Media devices
* JavaScript behavior

MCP itself does not automatically make a browser fingerprint different.

The relationship is:

```text id="mcp022"
MCP
 ↓
Browser Automation
 ↓
Browser Profile
 ↓
Fingerprint
 ↓
Website
```

Fingerprint management belongs to the browser/profile layer.

See:

[Browser Fingerprinting](../docs/browser-fingerprinting.md)

---

# MCP and Fingerprint Consistency

AI agents can perform long workflows.

For example:

```text id="mcp023"
Open
 ↓
Login
 ↓
Search
 ↓
Navigate
 ↓
Submit
 ↓
Verify
```

A stable browser environment can make these workflows easier to understand and troubleshoot.

The objective is not to make the browser invisible.

The objective is to maintain a coherent browser environment.

See:

[Fingerprint Consistency](../docs/fingerprint-consistency.md)

---

# MCP and Proxies

Network configuration is another layer that can be managed independently.

A browser automation system can use:

```text id="mcp024"
AI Agent
    ↓
MCP
    ↓
Browser
    ↓
Proxy
    ↓
Website
```

A more advanced architecture could include a proxy-management tool:

```text id="mcp025"
MCP
 └── Network Tools
       ├── get_proxy()
       ├── assign_proxy()
       ├── check_status()
       └── release_proxy()
```

The exact tool design depends on the infrastructure.

See:

[AI Agents and Proxies](ai-agents-and-proxies.md)

---

# MCP Does Not Automatically Manage Proxies

It is important not to confuse the MCP layer with the underlying infrastructure.

MCP can expose a proxy-management function.

It does not inherently provide:

* Proxy servers
* Residential IPs
* Mobile IPs
* Proxy rotation
* Network anonymity

Those capabilities must come from the underlying network infrastructure.

A useful model is:

```text id="mcp026"
AI Agent
    ↓
MCP
    ↓
Network Manager
    ↓
Proxy Infrastructure
```

---

# MCP + Anti-Detect Browsers

MCP can also be used as a tool interface for an anti-detect browser environment.

Conceptually:

```text id="mcp027"
AI Agent
    ↓
MCP
    ↓
Anti-Detect Browser
    ↓
Browser Profile
    ├── Fingerprint
    ├── Cookies
    └── Session
          ↓
        Proxy
          ↓
       Website
```

This creates a layered architecture:

| Layer               | Responsibility             |
| ------------------- | -------------------------- |
| AI Agent            | Reasoning                  |
| MCP                 | Tool interface             |
| Anti-detect browser | Browser-profile management |
| Profile             | Session/environment state  |
| Fingerprint         | Browser characteristics    |
| Proxy               | Network routing            |
| Website             | Destination                |

Each component solves a different problem.

---

# MCP and MarketerBrowser

MarketerBrowser includes MCP-related browser automation capabilities as part of its broader browser automation architecture.

A conceptual integration looks like:

```text id="mcp028"
AI Agent
    ↓
MCP
    ↓
MarketerBrowser
    ↓
Browser Profile
    ├── Fingerprint
    ├── Cookies
    └── Session State
    ↓
Network
    ↓
Website
```

This makes MCP useful as a bridge between AI agents and browser-profile infrastructure.

The important concept is not that MCP replaces the browser.

Instead:

> MCP connects AI systems to browser capabilities.

---

# Browser Use Through MCP

An AI agent can potentially use MCP browser tools to perform tasks such as:

```text id="mcp029"
Navigate to a website
        ↓
Inspect the page
        ↓
Find relevant content
        ↓
Click a link
        ↓
Read the next page
        ↓
Extract information
```

This is sometimes referred to as **AI browser use**.

The browser becomes one of the tools available to the agent.

See:

[Browser Use](browser-use.md)

---

# MCP Browser Automation for Research

Research is a natural application for browser agents.

An agent might:

```text id="mcp030"
Receive research question
        ↓
Search web
        ↓
Open sources
        ↓
Read pages
        ↓
Extract relevant information
        ↓
Compare sources
        ↓
Generate report
```

MCP can provide the browser tools required for this workflow.

For production systems, additional controls should be added around:

* Source validation
* Rate limits
* Logging
* Error handling
* Data storage
* Website policies

---

# MCP Browser Automation for QA

MCP can also connect AI agents to browser-testing environments.

A QA workflow could look like:

```text id="mcp031"
Test Objective
      ↓
AI Agent
      ↓
MCP
      ↓
Browser
      ↓
Application
      ↓
Test Result
```

The agent might inspect:

* Login forms
* Navigation
* Validation
* Checkout workflows
* Error states
* Dynamic components

The system can then record the result.

AI does not eliminate deterministic testing.

Instead, it can complement existing testing frameworks.

---

# MCP Browser Automation for E-Commerce

AI browser agents can assist with legitimate e-commerce workflows such as:

* Product research
* Catalog verification
* Price comparison
* Inventory checks
* Administrative workflows
* Localization testing

For example:

```text id="mcp032"
Product Research Task
       ↓
AI Agent
       ↓
MCP
       ↓
Browser
       ↓
Multiple Product Pages
       ↓
Structured Comparison
```

Official APIs should generally be preferred when they provide the required functionality.

---

# MCP Browser Automation for Web Testing

Browser-based testing can include:

* Responsive layout testing
* Form testing
* Navigation testing
* Localization testing
* Browser compatibility
* Regression testing

An AI agent can provide flexible interpretation of the current page while deterministic automation can handle repeatable checks.

---

# MCP and Authentication

Authentication requires additional care.

Browser agents may encounter:

* Login pages
* Session cookies
* Multi-factor authentication
* Verification challenges
* Expired sessions

A profile can preserve session state where appropriate.

However, authentication information should remain protected.

Do not expose passwords or session secrets unnecessarily to an AI model.

A safer architecture is:

```text id="mcp033"
AI Agent
    ↓
Approved Authentication Tool
    ↓
Browser Profile
    ↓
Authenticated Session
```

The AI does not need direct access to the underlying secret.

---

# MCP Security

MCP browser automation introduces an important security question:

> What can the AI agent actually do?

If an MCP server exposes unrestricted browser control, the agent may potentially access any website available to that browser.

Therefore, permission boundaries matter.

Useful controls include:

* Allowed domains
* Tool restrictions
* Profile restrictions
* Credential isolation
* Action approval
* Network restrictions
* Logging
* Session limits

---

# Least Privilege

A browser agent should receive the smallest set of permissions necessary.

For example:

```text id="mcp034"
Research Agent

Allowed:
✓ Navigate public pages
✓ Read page content
✓ Take screenshots

Restricted:
✗ Change account settings
✗ Access passwords
✗ Make purchases
✗ Delete data
```

This is safer than giving every agent unrestricted browser access.

---

# Human-in-the-Loop MCP Automation

Some actions should require human approval.

A useful architecture is:

```text id="mcp035"
AI Agent
    ↓
MCP
    ↓
Sensitive Action?
    ↓
Yes
    ↓
Human Approval
    ↓
Execute
```

Potential examples include:

* Purchases
* Account deletion
* Financial transactions
* Publishing
* Security changes
* Legal agreements

The objective should be controlled automation, not unlimited autonomy.

---

# Error Handling

MCP browser workflows can fail at multiple layers.

For example:

```text id="mcp036"
AI Error
Browser Error
Network Error
Tool Error
Website Error
Authentication Error
```

A production system should distinguish these failure types.

For example:

```text id="mcp037"
Tool Call
    ↓
Success?
 ┌──┴──┐
Yes    No
 ↓      ↓
Next   Diagnose
        ↓
      Retry?
       ↓
   Recover / Escalate
```

Useful mechanisms include:

* Timeouts
* Retries
* Validation
* Screenshots
* Structured error messages
* Logging
* Recovery procedures

---

# Observability

When AI controls a browser, developers need visibility into what happened.

Useful logs can include:

```text id="mcp038"
Timestamp
Agent ID
Profile ID
Tool Called
Parameters
Browser State
Result
Error
Duration
```

A browser screenshot can also be captured when an important operation fails.

Observability becomes increasingly important as the number of agents grows.

---

# MCP Browser Automation at Scale

A larger deployment may look like:

```text id="mcp039"
                  AI Controller
                       │
                       ▼
                    Task Queue
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
       Agent A      Agent B      Agent C
          │            │            │
          ▼            ▼            ▼
        MCP          MCP          MCP
          │            │            │
          ▼            ▼            ▼
      Browser A    Browser B    Browser C
          │            │            │
          ▼            ▼            ▼
       Profile A    Profile B    Profile C
```

Scaling introduces additional requirements:

* CPU
* RAM
* Storage
* Browser lifecycle management
* Network bandwidth
* Proxy capacity
* Logging
* Monitoring
* Task scheduling

AI browser automation is therefore an infrastructure problem as well as an AI problem.

---

# MCP vs Direct API Integration

MCP is not always necessary.

If a service provides a well-designed API, direct API access can often be simpler and more efficient.

For example:

```text id="mcp040"
AI Agent
    ↓
Official API
    ↓
Service
```

instead of:

```text id="mcp041"
AI Agent
    ↓
MCP
    ↓
Browser
    ↓
Website
```

Browser automation is particularly useful when the browser interface itself is important or when no suitable API is available.

---

# MCP vs Traditional Automation

| Approach       | Main Characteristic             |
| -------------- | ------------------------------- |
| Script         | Fixed sequence                  |
| Selenium       | Browser automation              |
| Playwright     | Modern browser automation       |
| Puppeteer      | Chromium automation             |
| RPA            | Structured business automation  |
| MCP            | AI-to-tool interface            |
| AI Agent + MCP | Adaptive tool-driven automation |

These technologies can be combined rather than treated as competitors.

For example:

```text id="mcp042"
AI Agent
    ↓
MCP
    ↓
Playwright
    ↓
Browser
```

---

# MCP Browser Automation and Fingerprint Testing

MCP can also expose browser-testing capabilities.

An agent could potentially:

```text id="mcp043"
Open fingerprint test
       ↓
Collect browser information
       ↓
Analyze results
       ↓
Compare with expected configuration
       ↓
Generate report
```

This can be useful for QA and browser-environment validation.

Testing should use measurable observations rather than claims such as "100% undetectable."

See:

[Browser Fingerprint Testing](../tests/fingerprint-tests.md)

---

# Responsible Use

Browser automation can be powerful.

That means it should be used responsibly.

Good use cases include:

* QA
* Web research
* Localization testing
* E-commerce administration
* Internal workflows
* Accessibility testing
* Software testing
* Content operations where permitted

Automation should respect:

* Website terms
* API policies
* Rate limits
* Privacy requirements
* Applicable laws
* Account permissions

MCP does not change these responsibilities.

---

# Common MCP Browser Automation Mistakes

## Mistake 1: Giving the Agent Full Browser Access

Unrestricted access increases the potential impact of mistakes.

Use permissions and tool restrictions.

---

## Mistake 2: Exposing Credentials

Passwords, cookies, API keys, and proxy credentials should not be unnecessarily exposed to the AI model.

---

## Mistake 3: Treating MCP as the Automation Framework

MCP is an interface layer.

Playwright, Puppeteer, Selenium, or another browser system may perform the actual browser operations.

---

## Mistake 4: Ignoring Browser Profiles

Persistent browser workflows often depend on session state.

---

## Mistake 5: Ignoring Network Configuration

Browser automation and network infrastructure are separate layers.

---

## Mistake 6: Assuming AI Always Makes the Correct Decision

AI agents can make mistakes.

Use validation and human approval where appropriate.

---

## Mistake 7: No Logging

When an autonomous workflow fails, developers need to understand what happened.

---

## Mistake 8: Using Browser Automation When an API Is Better

If an official API provides the required functionality, it may be preferable to controlling a browser.

---

# Best Practices

For MCP browser automation:

1. **Keep MCP tools narrowly scoped.**
2. **Use least-privilege permissions.**
3. **Separate AI reasoning from browser execution.**
4. **Use isolated browser profiles where required.**
5. **Protect credentials and session information.**
6. **Keep browser environments consistent.**
7. **Treat proxies as a separate network layer.**
8. **Add validation after important actions.**
9. **Implement timeouts and retries.**
10. **Log tool calls and browser results.**
11. **Capture screenshots when useful for debugging.**
12. **Use human approval for high-impact actions.**
13. **Monitor CPU, RAM, storage, and network usage.**
14. **Prefer official APIs when they provide a suitable alternative.**
15. **Follow website policies and applicable laws.**

---

# A Complete MCP Browser Architecture

A mature AI browser system could look like:

```text id="mcp044"
                           AI Model
                              │
                              ▼
                           AI Agent
                              │
                              ▼
                         MCP Client
                              │
                              ▼
                         MCP Server
                              │
                 ┌────────────┼────────────┐
                 ▼            ▼            ▼
            Browser Tool  Profile Tool  Network Tool
                 │            │            │
                 ▼            ▼            ▼
             Browser      Profiles      Proxy Manager
                 │            │            │
                 └────────────┼────────────┘
                              ▼
                       Browser Session
                              │
                              ▼
                           Website
```

This architecture makes the responsibilities clear.

---

# Where MarketerBrowser Fits

MarketerBrowser can serve as the browser infrastructure layer in an MCP-powered AI automation stack.

A conceptual architecture is:

```text id="mcp045"
AI Model
    ↓
AI Agent
    ↓
MCP
    ↓
MarketerBrowser
    ↓
Browser Profile
    ├── Fingerprint
    ├── Cookies
    └── Session State
    ↓
Network / Proxy
    ↓
Website
```

The important distinction is:

**AI agent:** decides what should happen.

**MCP:** provides the tool interface.

**MarketerBrowser:** provides browser-profile infrastructure.

**Browser profile:** maintains the browser environment and session.

**Proxy:** provides network routing.

This layered architecture makes it easier to understand where each component belongs.

---

# The Future of MCP Browser Automation

AI is moving from systems that only generate information toward systems that can interact with software.

Browser automation is an important part of that transition because the web is one of the largest software interfaces in existence.

A future browser automation stack may increasingly combine:

```text id="mcp046"
AI Models
+
AI Agents
+
MCP
+
Browser Automation
+
Browser Profiles
+
Network Infrastructure
+
Human Oversight
```

The goal is not simply to make browsers autonomous.

The more useful goal is to create **controlled, observable, reliable AI systems that can interact with the web**.

---

# Frequently Asked Questions

## What is MCP browser automation?

MCP browser automation is an architecture where browser-control capabilities are exposed to an AI system through Model Context Protocol tools.

## Does MCP control the browser directly?

Usually, MCP acts as an interface between the AI system and tools that control the browser.

The underlying browser automation may be provided by Playwright, Puppeteer, Selenium, or another system.

## Can MCP work with Playwright?

Yes. Playwright can serve as the browser automation layer underneath an MCP interface.

## Can MCP work with Puppeteer?

Yes. Puppeteer can provide the underlying Chromium automation capabilities.

## Can MCP work with Selenium?

Yes. Selenium can serve as the browser automation layer in an MCP-based architecture.

## Does MCP provide a browser?

No.

MCP is a protocol/interface layer. A separate browser and automation implementation are still required.

## Does MCP provide proxies?

No.

MCP can expose proxy-management tools if an implementation provides them, but the actual proxy infrastructure comes from a separate network system.

## Does MCP change browser fingerprints?

Not inherently.

Fingerprint management belongs to the browser/profile layer.

## Can MCP manage browser profiles?

It can, if the connected browser infrastructure exposes profile-management capabilities through MCP tools.

## Can AI agents use MCP to control multiple browsers?

Yes, provided the MCP implementation and underlying browser infrastructure support multiple browser instances or profiles.

## Is MCP the same as RPA?

No.

RPA focuses on automating business processes. MCP provides a standardized interface through which AI systems can interact with external tools.

They can be used together.

## Is MCP required for AI browser automation?

No.

AI browser agents can be built without MCP.

MCP is useful when a standardized tool interface is desirable.

## Is MCP browser automation secure?

Security depends heavily on the implementation.

Important considerations include:

* Tool permissions
* Domain restrictions
* Credential isolation
* Profile isolation
* Logging
* Human approval
* Network controls

## Can MCP browser agents work autonomously?

They can perform multi-step workflows autonomously when the underlying tools and permissions allow it.

However, human oversight may still be appropriate for sensitive operations.

---

# Conclusion

MCP provides an important bridge between AI systems and external tools.

For browser automation, that bridge can look like:

```text id="mcp047"
AI Model
    ↓
AI Agent
    ↓
MCP
    ↓
Browser Tools
    ↓
Automation Framework
    ↓
Browser
    ↓
Profile
    ↓
Network
    ↓
Website
```

MCP does not replace browsers, browser automation frameworks, profiles, fingerprints, or proxies.

Instead, it can connect these components to an AI agent through a structured tool interface.

That makes MCP particularly interesting for the next generation of browser automation, where AI systems do not simply generate instructions but can observe, reason, act, verify, and continue working through real software interfaces.

---

## Related Topics

* [AI Browser Agents](ai-browser-agents.md)
* [Browser Use](browser-use.md)
* [AI Agents and Fingerprints](ai-agents-and-fingerprints.md)
* [AI Agents and Proxies](ai-agents-and-proxies.md)
* [Autonomous Browser Workflows](autonomous-browser-workflows.md)
* [Browser Automation](../automation/browser-automation.md)
* [Playwright](../automation/playwright.md)
* [Puppeteer](../automation/puppeteer.md)
* [Selenium](../automation/selenium.md)
* [Browser Fingerprinting](../docs/browser-fingerprinting.md)
* [Browser Profile Isolation](../docs/browser-profile-isolation.md)
* [Fingerprint Consistency](../docs/fingerprint-consistency.md)
* [Proxy and Browser Fingerprint](../proxy/proxy-and-browser-fingerprint.md)
* [Browser Fingerprint Testing](../tests/fingerprint-tests.md)
