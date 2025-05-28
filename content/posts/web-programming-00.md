+++
date = '2025-05-21T17:15:36+09:00'
title = '[Web Programming] [00] Introduction to Web Programming'
description = "The history of web and core concepts of web programming."
categories = ["Information Technology/Application Software Development/Web Programming"]
tags = ["FrontEnd", "Backend"]
slug = "introduction-to-web-programming"
math = true
draft = false
+++

# Chapter 00. Introduction to Web Programming

> **Outline:** This chapter provides an overview of the World Wide Web, its evolution, and the core technologies that make it work, such as HTML, URL, and HTTP. 
It also explains the role of the W3C, the difference between the Web and the Internet, and how browsers, servers, and developers interact within the web ecosystem.

---

## Contents
- [0.1. What is the World Wide Web (WWW)?](#section-01-what-is-the-world-wide-web-www)
- [0.2. A Brief History of the Web (Web 1.0 → Web 3.0)](#section-02-a-brief-history-of-the-web)
- [0.3. What is the W3C?](#section-03-what-is-the-w3c)
- [0.4. Core Technologies of the Web](#section-04-core-technologies-of-the-web)
- [0.5. Web Architecture](#section-05-web-architecture-client--server--network)
- [0.6. What is a Web Browser?](#section-06-what-is-a-web-browser)
- [0.7. Web Development Workflow](#section-07-web-development-workflow)
- [0.8. Domain & Hosting Basics *(Optional)*](#section-08-domain--hosting-basics-optional)

---

## Section 0.1. What is the World Wide Web (WWW)?

### 1. Definition
The **World Wide Web (WWW)** — often simply called **"the Web"** — is a global information system based on **hypertext** that allows users to access and navigate resources over the **Internet** using a **web browser**.
  - It is a **service that runs on top of the Internet**.
  - It is a system of interlinked **HTML documents** accessed via web browsers using the **HTTP protocol**.

> In simple terms: everything you view in your web browser (like websites) exists on the World Wide Web.

---

### 2. Key Components
The Web relies on three foundational technologies:

| Component | Description |
|----------|-------------|
| **HTML** | Defines the structure and content of web pages (HyperText Markup Language) |
| **URL**  | Specifies the address of resources on the Web (Uniform Resource Locator) |
| **HTTP** | Protocol used for communication between browsers and servers (HyperText Transfer Protocol) |

---

### 3. Key Characteristics
- **Hypertext-based**: Resources are interconnected through hyperlinks.
- **Distributed system**: Web content is hosted across servers around the world.
- **Standardized**: Organizations like **W3C** (World Wide Web Consortium) define and maintain web standards.

---

### 4. WWW vs Internet
- The **Internet** is the **infrastructure** (network of connected computers).
  - It provides the physical and technical infrastructure that allows devices to communicate and exchange data.
  - It includes cables, routers, satellites, wireless signals, and protocols like IP and TCP.
- The **Web** is a **service** that runs on top of the Internet to share information using browsers.
  - Examples of Internet-based services include email, cloud storage, online games, and VoIP.


#### Key Differences

| Aspect        | Internet                                 | World Wide Web                         |
|---------------|------------------------------------------|----------------------------------------|
| Definition     | Global network infrastructure            | Information-sharing system on top of the Internet |
| Function       | Transfers all types of data              | Displays and navigates HTML documents  |
| Components     | Routers, cables, IP, TCP, etc.           | HTML, HTTP, URL, browsers              |
| Examples       | Email, FTP, Cloud storage, VoIP          | Websites, blogs, web applications      |


**Analogy:**  
- Internet = Roads and highways
- WWW      = Cars traveling on those roads

---

### 5. Simple Example
If the **Internet** is the entire subway system,  
then the **WWW** is just one of the lines — used to transport information (webpages).

---

## Section 0.2. A Brief History of the Web

### 1. The Birth of the Web
- In **1989**, **Tim Berners-Lee** at **CERN** proposed a hypertext-based system for sharing information.
- In **1991**, the **first website** was launched: [info.cern.ch](http://info.cern.ch)

---

### 2. The Three Generations of the Web

#### Web 1.0 – The Static Web (1990s ~ early 2000s)
- Mostly **read-only** content.
- Static HTML pages with minimal interaction.
- Users are passive consumers.
- Examples: early company websites, basic portals.

#### Web 2.0 – The Social Web (2000s ~ 2020)
- **Read and write** capabilities for users.
- Interactive sites with blogs, comments, and social media.
- Technologies: JavaScript, AJAX, REST APIs.
- Examples: YouTube, Facebook, Wikipedia.

#### Web 3.0 – The Semantic/Decentralized Web (2020 ~ )
- AI-driven and **decentralized** web services.
- Focuses on **data ownership**, meaning, and smart contracts.
- Technologies: Blockchain, Semantic Web (RDF, OWL).
- Examples: Ethereum, DApps, MetaMask.

---

### 3. Summary of the Evolution

| Feature     | Web 1.0            | Web 2.0                   | Web 3.0                          |
|-------------|--------------------|---------------------------|----------------------------------|
| Structure   | Static             | Dynamic                   | Semantic / Decentralized        |
| Users       | Consumers          | Producers + Consumers     | Data Owners / Autonomous Users  |
| Technologies| HTML, HTTP, URL    | JS, AJAX, REST API        | Blockchain, AI, RDF             |
| Examples    | Yahoo, Geocities   | YouTube, Instagram        | MetaMask, DApps                 |

---

### 4. Conceptual Flow
|Web 1.0             |Web 2.0            |Web 3.0                        |
|--------------------|-------------------|-------------------------------|
|Information Sharing |User Participation |Decentralized & Meaningful Data|

---

## Section 0.3. What is the W3C?

### 1. Definition
The **W3C (World Wide Web Consortium)** is the main international organization responsible for developing and maintaining web standards.  
It was founded in **1994** by **Tim Berners-Lee**, the inventor of the Web.

> W3C ensures that all browsers and websites follow consistent rules so the Web functions reliably across platforms.

---

### 2. Purpose
- Standardization of core web technologies (HTML, CSS, XML, DOM, etc.)
- Ensuring accessibility for all users, including people with disabilities
- Supporting the long-term growth and openness of the Web
- Promoting cross-browser compatibility and interoperability

---

### 3. Major Activities
- Publishing official web standards (W3C Recommendations)
- Managing working groups in areas like HTML, CSS, Accessibility, Web Security
- Providing validation tools (e.g., HTML/CSS validators)
- Encouraging open, royalty-free web technologies

> Examples
> **HTML5** was co-developed by W3C and WHATWG  
> **CSS3** is maintained by W3C's CSS Working Group

---

### 4. Why Web Standards Matter
- Ensure consistent behavior of web pages across different browsers and devices
- Enable developers to build with predictable, reliable outcomes
- Prevent proprietary control by maintaining open and neutral standards

---

## Section 0.4. Core Technologies of the Web

### Overview
The Web relies on three core technologies that form its foundation:

1. **HTML** – HyperText Markup Language  
2. **URL** – Uniform Resource Locator  
3. **HTTP** – HyperText Transfer Protocol

---

### 1. HTML – Structure of Web Pages

- HTML is a markup language used to define the **structure and content** of a web page.
- It uses **tags** to mark elements like text, images, links, tables, and more.

> Example: `<p>Welcome!</p>` represents a paragraph.

- Web browsers read HTML and **render** it for the user.

> More explanations > [HTMl]({{< relref "posts/web-programming-01.md" >}})

---

### 2. URL – Addressing System

- A **URL** specifies the **location** of a resource on the Web.
- It tells the browser where to find an HTML document, image, or other file.

> Example format: `https://www.example.com:443/path/to/page.html?query=keyword#section1`

- URL components:

| Component            | Description                  |
|----------------------|------------------------------|
| `https`              | Protocol (with encryption)   |
| `www.example.com`    | Domain name                  |
| `:443`               | Port number (optional)       |
| `/path/to/page.html` | Path to resource             |
| `?query=keyword`     | Query parameters             |
| `#section1`          | Fragment identifier          |

---

### 3. HTTP – Communication Protocol
- HTTP is the foundational protocol used for communication between **clients (e.g., web browsers)** and **web servers** on the World Wide Web.
- It defines how requests are sent and how responses are returned.
> HTTPS = HTTP + SSL/TLS encryption

---

- Common HTTP methods:
| Method   | Description                              |
|----------|------------------------------------------|
| `GET`    | Retrieve a resource (e.g., load a page)  |
| `POST`   | Submit data to the server (e.g., form)   |
| `PUT`    | Update a resource entirely               |
| `PATCH`  | Update part of a resource                |
| `DELETE` | Remove a resource                        |
| `HEAD`   | Request only the headers (no body)       |

---

- Example of a Request

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Chrome/117.0
Accept: text/html
```

- Example of a Response
```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html>
  <body>Hello, world!</body>
</html>
```
---

- HTTP status codes:

| Code | Status Text               | Meaning                                      |
|------|---------------------------|----------------------------------------------|
| 200  | OK                        | Request succeeded                            |
| 201  | Created                   | Resource successfully created                |
| 204  | No Content                | Request succeeded, no content returned       |
| 301  | Moved Permanently         | Resource moved to a new permanent URI        |
| 302  | Found                     | Resource temporarily moved                   |
| 304  | Not Modified              | Cached version is still valid                |
| 400  | Bad Request               | Malformed or invalid request                 |
| 401  | Unauthorized              | Authentication required                      |
| 403  | Forbidden                 | Access to the resource is denied             |
| 404  | Not Found                 | Resource not found                           |
| 405  | Method Not Allowed        | HTTP method not supported for this resource  |
| 500  | Internal Server Error     | Generic server error                         |
| 502  | Bad Gateway               | Invalid response from an upstream server     |
| 503  | Service Unavailable       | Server temporarily overloaded or down        |
| 504  | Gateway Timeout           | Upstream server failed to respond in time    |

---

## Section 0.5. Web Architecture (Client / Server / Network)

### 1. Basic Components

The Web operates on a three-part architecture involving:

1. **Client**  
   - The user's **web browser or application**
   - Requests web content and **renders** HTML, CSS, and JavaScript

2. **Server**  
   - A **remote machine** that receives requests and sends back data
   - Often built using technologies like Node.js, Python, PHP, Java, etc.

3. **Network**  
   - The **communication channel** between client and server
   - Operates over protocols like **HTTP** and **TCP/IP**

---

### 2. How the Web Works (Request–Response Flow)

- Step 01: User enters URL into the browser
- Step 02: Browser resolves domain to an IP address via DNS
- Step 03: Browser send an HTTP request to server (e.g., GET)
- Step 04: Web server processes the request and sends a response with HTML/CSS/JS
- Step 05: Browser renders HTML, CSS, JavaScript
- Step 06: Web page is displayed to the user

| Step               | Description                             |
|--------------------|------------------------------------------|
| **URL Input**      | e.g., `https://example.com`             |
| **DNS Resolution** | Converts domain name to IP address      |
| **HTTP Request**   | Example: `GET /index.html HTTP/1.1`     |
| **Server Response**| Returns HTML, CSS, JS, status code      |
| **Rendering**      | Build DOM, apply CSS, run JS            |
| **Final Output**   | Web page is displayed on screen         |

> Rendering Process Inside the Browser (**Critical Rendering Path**)
> 1. **HTML** → DOM Tree  
> 2. **CSS** → CSSOM Tree  
> 3. **DOM + CSSOM** → Render Tree  
> 4. Layout → Paint → Composite → Visual Display

---

### 3. Client vs Server: Role Comparison

| Role         | Client (Browser/App)                      | Server (Web Server)                            |
|--------------|-------------------------------------------|------------------------------------------------|
| Location     | Local device                              | Remote machine                                 |
| Responsibilities | Send requests, render content, handle UI | Process logic, respond with data, host files    |
| Examples     | Chrome, Safari, Mobile App                | Node.js, Apache, Nginx, Flask, Django, etc.     |

---

### 4. Communication Layers (TCP/IP Stack)

Web communication typically follows the **TCP/IP 4-layer model**:
> The **TCP/IP model** (Transmission Control Protocol / Internet Protocol) is a standardized framework that describes how data is transmitted across computer networks.

- **Application Layer** (Layer 4)
  - Closest to the **user and application software**.
  - Provides services like **web browsing**, **file transfer**, and **email**.
  - Common protocols: **HTTP**, **HTTPS**, **FTP**, **DNS**, **SMTP**
- **Transport Layer** (Layer 3)
  - Provides **end-to-end communication** and data flow control.
  - Key protocols:
    - **TCP** (Transmission Control Protocol): Reliable, ordered delivery
    - **UDP** (User Datagram Protocol): Fast, connectionless delivery
  - Handles **port numbers**, **error checking**, and **retransmissions**.
- **Internet Layer** (Layer 2)
  - Manages **logical addressing** and **routing** between networks.
  - Uses **IP addresses** to find destination devices.
  - Handles **packet delivery**, **fragmentation**, and **reassembly**.
  - Protocols: **IP**, **ICMP**, **ARP**
- **Network Access Layer** (Layer 1)
  - Also known as: **Link Layer** or **Data Link Layer**
  - Handles the **physical transmission** of data over a network.
  - Responsible for **hardware addressing (MAC addresses)** and data framing.
  - Common technologies: **Ethernet**, **Wi-Fi**, **PPP**

---

## Section 0.6. What is a Web Browser?

### 1. Definition
A **web browser** is a **software application** that enables users to access, retrieve(가져오다), and interact with information on the **World Wide Web**.

---

### 2. Key Functions

| Function            | Description |
|---------------------|-------------|
| **URL Requesting**  | Sends an HTTP request based on the URL the user enters |
| **Page Rendering**  | Displays HTML, CSS, and JavaScript content visually |
| **JavaScript Execution** | Handles interactivity and dynamic behavior |
| **Caching & Cookies**   | Stores files and user data for faster access |
| **Developer Tools**     | Helps with debugging and inspecting the DOM, network, console, etc. |

---

### 3. Main Components of a Browser

| Component              | Role |
|------------------------|------|
| **User Interface**     | Address bar, tabs, buttons, etc. |
| **Browser Engine**     | Coordinates between the UI and rendering engine |
| **Rendering Engine**   | Parses HTML/CSS and paints the page (e.g., Blink, WebKit) |
| **JavaScript Engine**  | Executes JavaScript code (e.g., V8, SpiderMonkey) |
| **Networking**         | Handles HTTP requests and responses |
| **Data Storage**       | Manages cache, cookies, localStorage, sessionStorage |

---

### 4. Popular Browsers & Their Engines

| Browser   | Rendering Engine | JavaScript Engine |
|-----------|------------------|-------------------|
| Chrome    | Blink             | V8                |
| Safari    | WebKit            | JavaScriptCore    |
| Firefox   | Gecko             | SpiderMonkey      |

---

### 5. Why It Matters

- A **frontend developer** must understand how browsers work to build reliable web apps.
- Helps with fixing **cross-browser issues** and handling **inconsistent feature support**.
- Performance and user experience can vary greatly depending on how a browser renders content.

---

## Section 0.7. Web Development Workflow

> Web development is more than just writing HTML—it involves a full cycle of planning, coding, testing, deploying, and maintaining a project.

---

### 1. Typical Workflow Steps

| Step             | Description                                               |
|------------------|-----------------------------------------------------------|
| **Planning**     | Define layout, features, and user flow                    |
| **Development**  | Build structure (HTML), style (CSS), and interactivity (JS) |
| **Testing**      | Check browser compatibility, responsiveness, performance  |
| **Deployment**   | Publish to a live server (e.g., GitHub Pages, Netlify)    |
| **Maintenance**  | Bug fixes, updates, improvements based on feedback        |

---

### 2. Essential Tools

| Tool/Environment    | Purpose                                   |
|---------------------|-------------------------------------------|
| **VS Code**         | Code editor with extensions and Git support |
| **Browser DevTools**| Inspect HTML/CSS, debug JS, monitor network |
| **Git & GitHub**    | Version control and collaboration         |
| **Terminal / CLI**  | Command-line tasks like building and serving |
| **Live Server**     | Local preview with auto-reload            |

---

### 3. Sample Folder Structure

my-project/
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── main.js
├── images/
│   └── logo.png
├── README.md
└── .gitignore

---

### 4. Simple Deployment Options

- **Static Site Hosting**:
  - GitHub Pages
  - Netlify
  - Vercel

- **Dynamic Hosting Platforms**:
  - Firebase, Render, AWS, Heroku

---

### 5. Developer Checklist

- [ ] Use semantic HTML structure
- [ ] Write modular, responsive CSS
- [ ] Check for JavaScript console errors
- [ ] Test accessibility and performance (e.g., Lighthouse)
- [ ] Use clear Git commit messages

---

## Section 0.8. Domain & Hosting Basics (Optional)

### 1. What is a Domain?

- A **domain** is the human-readable address of a website.
- Example: In `https://www.google.com`, the domain is `google.com`.
- Domains are translated into actual server **IP addresses** using the **DNS (Domain Name System)**.

> `google.com` → `142.250.206.206`

---

### 2. What is Hosting?

- **Hosting** is the service of storing and serving your website files (HTML, CSS, JS) on a **web server**.
- The server is always connected to the Internet and responds to browser requests.

> Think of **domain as an address**, and **hosting as the physical house**.

---

### 3. How Domain & Hosting Work Together

1.	User types a domain in the browser (e.g., www.example.com)
2.	DNS resolves the domain to an IP address
3.	HTTP request is sent to the corresponding server
4.	Server responds with HTML/CSS/JS → Web page is rendered

---

### 4. Free Domain/Hosting Options

| Platform       | Domain Style              | Hosting Available | Features                          |
|----------------|---------------------------|:-------------------:|-----------------------------------|
| GitHub Pages   | `username.github.io`      | O                | Free static site hosting          |
| Netlify        | `*.netlify.app`           | O                | Fast deployment, CI/CD support    |
| Vercel         | `*.vercel.app`            | O                | Great for Next.js, static hosting |
| Firebase       | `*.web.app`, `*.firebaseapp.com` | O       | Supports static and dynamic sites |

---

### 5. Paid Domain & Hosting Options

- **Domain registrars**: GoDaddy, Google Domains, Namecheap
- **Hosting providers**: AWS, Heroku, Render, Kinsta
- Useful for portfolios, blogs, and business websites

---

### 6. Basic Setup Workflow

1. Purchase or register a domain (or get a free subdomain)
2. Upload your site to a hosting platform
3. Configure DNS settings (e.g., A record, CNAME) to link domain with hosting

---