# Preserving Privacy

## 1. Privacy and Web Activity

Privacy is about controlling what information about you is exposed, to whom, and for what purpose.

Your online activity can leave records in several places:

- Your browser
- Websites and application servers
- Internet service providers
- DNS providers
- Advertising and analytics services
- Operating systems and installed applications

Clearing your local browser history does **not** erase records that already exist on remote servers.

---

## 2. Web Browsing History

A browser can remember the websites you visited, while servers can maintain their own activity logs.

A typical server log may contain information such as:

- IP address
- Time of request
- Requested resource
- HTTP status code
- Referring page
- User-Agent

### Important point

Deleting local browsing history mainly affects the information stored on your own device. It does not automatically remove server-side logs.

---

## 3. HTTP Headers

HTTP headers are key-value pairs exchanged between a browser and a web server.

Some headers can reveal information about your browsing activity.

### Referer header

When you follow a link, the browser may tell the destination website which page referred you.

For example:

```text
Referer: https://www.example.com/search?q=cats
```

This can expose more information than intended, such as a search URL.

### Limiting referrer information

Websites can use a referrer policy to reduce what is sent.

For example:

```html
<meta name="referrer" content="origin">
```

This can limit the information to the origin of the referring site.

A stricter policy can prevent referrer information from being sent:

```html
<meta name="referrer" content="no-referrer">
```

---

## 4. Browser Fingerprinting

Fingerprinting identifies or distinguishes a browser using a collection of characteristics.

Possible signals include:

- User-Agent
- Operating system
- Browser version
- Screen resolution
- Installed fonts
- Browser extensions
- Other browser or device characteristics
- IP address

### Why fingerprinting matters

One individual attribute may not uniquely identify someone. A large combination of attributes can make a browser more distinguishable.

### Key idea

Fingerprinting can still work even when a user deliberately limits some forms of information sharing.

---

## 5. Session Cookies

Cookies are small pieces of information stored by browsers and associated with websites.

A **session cookie** can allow a server to recognize a particular browsing session.

Example:

```text
Set-Cookie: session=1234abcd
```

The browser later sends the cookie back to the appropriate server.

### Properties of session cookies

- They can identify a session.
- Their lifetime is controlled by the server.
- They are commonly used for login sessions and application state.

---

## 6. Tracking Cookies

Tracking cookies can be used to associate activity with a user or browser over time.

For example:

```text
Set-Cookie: id=1234abcd; max-age=31536000
```

A long-lived identifier can allow activity to be associated with the same browser for an extended period.

### Difference

| Session cookie | Tracking cookie |
|---|---|
| Often supports a particular session | Often supports tracking over time |
| Usually shorter-lived | Can be long-lived |
| Commonly used for application state | Commonly used for analytics or advertising |

---

## 7. Tracking Parameters

Tracking information can also appear directly inside URLs.

Example:

```text
https://example.com/ad?click_id=ABC123&campaign_id=23
```

Here, `click_id` can act as an identifier associated with a particular interaction.

### Difference from cookies

- Cookies store tracking information in the browser.
- Tracking parameters put tracking information directly in URLs.

Removing unnecessary identifiers from URLs can reduce unnecessary exposure.

---

## 8. Third-Party Cookies

A third-party cookie is associated with a domain different from the main website a user is visiting.

### Example flow

1. You visit Website A.
2. Website A loads content from Company B.
3. Company B sets a cookie in your browser.
4. You later visit Website C that also loads content from Company B.
5. The same identifier may be sent again.
6. Company B can associate activity across the two sites.

This historically became an important mechanism for cross-site advertising and tracking.

---

## 9. Private Browsing

Private or incognito browsing mainly changes what is retained locally after the private session ends.

It can help prevent some local traces from being retained, but it is **not anonymity**.

During a private session:

- Websites can still see requests.
- Servers can still maintain logs.
- Network providers can still observe relevant traffic metadata.
- New cookies can still exist during the session.
- Fingerprinting can still occur.

### Key idea

Private browsing is primarily a local privacy feature, not a complete privacy or anonymity system.

---

## 10. Supercookies

A supercookie is a tracking mechanism that is difficult for users to remove using ordinary browser cookie controls.

A network provider can potentially inject or derive persistent identifiers through mechanisms outside ordinary browser cookie storage.

### Defensive idea

Reducing unnecessary tracking and using encrypted protocols can limit some forms of network-level observation.

---

## 11. DNS and Privacy

The **Domain Name System (DNS)** translates domain names such as:

```text
example.com
```

into IP addresses.

Traditional DNS commonly travels without encryption.

This means the DNS infrastructure or a network observer may be able to learn which domain your device is attempting to resolve.

### Encrypted DNS

Two common approaches are:

- **DNS over HTTPS (DoH)**
- **DNS over TLS (DoT)**

These protect DNS requests while they travel to the DNS resolver.

### Important limitation

Encrypted DNS does not make all internet activity anonymous. Other traffic metadata and the destination itself can still provide information.

---

## 12. VPNs

A **Virtual Private Network (VPN)** creates an encrypted connection between your device and a VPN server.

Basic flow:

```text
Your device
    |
    | Encrypted VPN tunnel
    v
VPN server
    |
    v
Internet
```

Websites generally see the VPN server's public IP address instead of your device's public IP address.

### What a VPN can help with

- Protecting traffic between your device and the VPN server
- Hiding your public IP address from destination websites
- Reducing exposure to some local network observers

### What a VPN does not guarantee

A VPN does not make you anonymous.

A VPN also does not protect a device from malware that is already running on it.

The VPN provider itself becomes an important party that you must trust.

---

## 13. Tor

Tor is an anonymity-oriented network that routes traffic through multiple relays.

Conceptually:

```text
User
  |
  v
Tor Relay 1
  |
  v
Tor Relay 2
  |
  v
Tor Relay 3
  |
  v
Destination
```

Traffic is routed through multiple encrypted hops rather than one directly visible path.

### Strengths

- Makes direct source tracing more difficult
- Distributes trust across multiple relays
- Designed to reduce the amount of information any single relay knows

### Limitations

- It does not provide absolute anonymity.
- Browser configuration and user behavior can still reveal identity.
- An observer may use timing or other metadata to make inferences.
- Unique behavior can make a user easier to identify.

### Important principle

No privacy technology provides perfect protection under every threat model.

---

## 14. Permissions

Modern operating systems and applications often request permission to access sensitive resources.

Examples include:

- Location
- Camera
- Microphone
- Contacts
- Photos and files
- Notifications
- Bluetooth

### Principle of least privilege

Grant an application only the permissions it actually needs.

For example, a calculator application generally should not require continuous access to your location.

### Good practice

Review permissions regularly and revoke unnecessary access.

---

## 15. Privacy Threat Model

Privacy decisions should be based on **what you are protecting, from whom, and at what cost**.

Ask:

1. What information am I trying to protect?
2. Who could access it?
3. What information can they observe?
4. How long could they retain it?
5. What privacy tools actually address that threat?
6. What usability or trust trade-offs do those tools introduce?

---

## 16. Browser Privacy Checklist

- Review browser privacy settings.
- Limit unnecessary cookies.
- Be careful with tracking parameters in URLs.
- Use appropriate referrer policies when developing websites.
- Keep browsers updated.
- Review installed extensions.
- Remove extensions you do not need.
- Review site permissions.
- Use encrypted DNS when appropriate.
- Understand the limits of private browsing.

---

## 17. Network Privacy Checklist

- Prefer HTTPS websites.
- Be cautious on untrusted networks.
- Understand what your ISP or network administrator can observe.
- Consider encrypted DNS.
- Understand what a VPN does and does not protect.
- Understand Tor's threat model before relying on it for anonymity.

---

## 18. Key Comparisons

| Technology | Primary purpose | Main limitation |
|---|---|---|
| Private browsing | Reduce local browser traces | Does not hide activity from websites or networks |
| Referrer policy | Control referrer information | Does not stop all tracking |
| Encrypted DNS | Protect DNS queries in transit | Does not hide all traffic metadata |
| VPN | Encrypt traffic to VPN server and hide public IP from destinations | Requires trust in VPN provider |
| Tor | Stronger network-level anonymity | Not perfect; behavior and metadata still matter |
| Cookie controls | Limit browser-stored identifiers | Other tracking mechanisms can remain |
| Permission controls | Restrict application access | Cannot protect information already shared |

---

## 19. Core Ideas to Remember

1. **Deleting local history does not delete server logs.**
2. **HTTP headers can reveal browsing context.**
3. **Browser fingerprinting combines multiple device and browser characteristics.**
4. **Cookies can maintain session state or support long-term tracking.**
5. **Tracking identifiers can appear in URLs as well as cookies.**
6. **Private browsing is not anonymity.**
7. **Traditional DNS can reveal the domains you request.**
8. **DoH and DoT encrypt DNS communication.**
9. **A VPN changes where traffic appears to originate, but creates a trust relationship with the VPN provider.**
10. **Tor distributes traffic across multiple relays to improve anonymity.**
11. **No privacy technology provides absolute protection.**
12. **Permissions should follow least privilege.**

---

## 20. Quick Revision

### Browsing History
Local history is only one record of your activity. Remote services may retain their own logs.

### HTTP Headers
Headers carry metadata between browser and server. Referrer information can reveal where a request originated.

### Fingerprinting
A browser can be identified using a combination of characteristics such as browser, OS, screen, extensions, fonts, and network information.

### Cookies
Cookies can identify sessions and can also be used for tracking.

### Tracking Parameters
URLs can carry identifiers that associate clicks or campaigns with users or sessions.

### Third-Party Cookies
Third parties can historically use shared resources and cookies to connect activity across websites.

### Private Browsing
Limits some local storage and history but does not make the user invisible.

### Supercookies
Persistent tracking techniques can exist outside normal browser cookie controls.

### DNS
DNS converts names to IP addresses. Traditional DNS may expose requested domains.

### VPN
Creates an encrypted tunnel to a VPN server and hides the user's public IP from many destinations.

### Tor
Routes traffic through multiple relays to provide stronger anonymity properties.

### Permissions
Applications should receive only the access they need.
