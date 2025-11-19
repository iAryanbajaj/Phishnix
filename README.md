<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NetForge - Custom TCP/IP Protocol Stack</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #1e40af;
            --primary-dark: #1e3a8a;
            --secondary: #3b82f6;
            --accent: #60a5fa;
            --light: #f0f9ff;
            --dark: #0f172a;
            --gray: #64748b;
            --light-gray: #f1f5f9;
            --white: #ffffff;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            line-height: 1.6;
            color: var(--dark);
            background-color: var(--light);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header Styles */
        header {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: var(--white);
            padding: 100px 0 80px;
            position: relative;
            overflow: hidden;
        }
        
        header::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="none" stroke="rgba(255,255,255,0.05)" stroke-width="1"/></svg>');
            background-size: 50px 50px;
            z-index: 1;
        }
        
        .header-content {
            position: relative;
            z-index: 2;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
        
        .logo {
            font-size: 3.5rem;
            margin-bottom: 20px;
            color: var(--white);
        }
        
        h1 {
            font-size: 3rem;
            font-weight: 700;
            margin-bottom: 15px;
            letter-spacing: -0.5px;
        }
        
        .subtitle {
            font-size: 1.25rem;
            font-weight: 400;
            margin-bottom: 30px;
            opacity: 0.9;
        }
        
        .author {
            font-size: 1.1rem;
            font-weight: 500;
            margin-bottom: 40px;
        }
        
        .badges {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .badge {
            background-color: rgba(255, 255, 255, 0.15);
            padding: 8px 15px;
            border-radius: 50px;
            font-size: 0.9rem;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        /* Navigation */
        nav {
            background-color: var(--white);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
        }
        
        .nav-logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
        }
        
        .nav-links {
            display: flex;
            gap: 25px;
        }
        
        .nav-links a {
            text-decoration: none;
            color: var(--dark);
            font-weight: 500;
            transition: color 0.3s;
        }
        
        .nav-links a:hover {
            color: var(--primary);
        }
        
        /* Main Content */
        main {
            padding: 60px 0;
        }
        
        .section {
            margin-bottom: 80px;
        }
        
        .section-title {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .section-title i {
            color: var(--secondary);
        }
        
        .section-content {
            background-color: var(--white);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
        }
        
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-top: 30px;
        }
        
        .feature-card {
            background-color: var(--light);
            border-radius: 10px;
            padding: 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
        }
        
        .feature-icon {
            font-size: 2.5rem;
            color: var(--secondary);
            margin-bottom: 15px;
        }
        
        .feature-title {
            font-size: 1.2rem;
            font-weight: 600;
            margin-bottom: 10px;
        }
        
        .feature-description {
            color: var(--gray);
        }
        
        /* Code Blocks */
        .code-block {
            background-color: var(--dark);
            color: var(--white);
            border-radius: 8px;
            padding: 20px;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
            position: relative;
        }
        
        .code-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .code-title {
            font-weight: 500;
            color: var(--accent);
        }
        
        .copy-btn {
            background-color: rgba(255, 255, 255, 0.1);
            border: none;
            color: var(--white);
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.85rem;
            transition: background-color 0.3s;
        }
        
        .copy-btn:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }
        
        /* Diagrams */
        .diagram {
            background-color: var(--light-gray);
            border-radius: 8px;
            padding: 25px;
            margin: 30px 0;
            text-align: center;
        }
        
        .diagram-title {
            font-weight: 600;
            margin-bottom: 20px;
            color: var(--primary);
        }
        
        .protocol-stack {
            display: flex;
            flex-direction: column;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .layer {
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 6px;
            font-weight: 500;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .layer-app {
            background-color: var(--accent);
            color: var(--white);
        }
        
        .layer-transport {
            background-color: var(--secondary);
            color: var(--white);
        }
        
        .layer-internet {
            background-color: var(--primary);
            color: var(--white);
        }
        
        .layer-link {
            background-color: var(--primary-dark);
            color: var(--white);
        }
        
        /* Screenshots */
        .screenshots {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 30px;
            margin: 40px 0;
        }
        
        .screenshot-card {
            background-color: var(--white);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
        }
        
        .screenshot-img {
            width: 100%;
            height: auto;
            display: block;
        }
        
        .screenshot-caption {
            padding: 20px;
            font-weight: 500;
            text-align: center;
            background-color: var(--light-gray);
        }
        
        /* Installation Steps */
        .steps {
            counter-reset: step;
            margin: 30px 0;
        }
        
        .step {
            position: relative;
            padding-left: 60px;
            margin-bottom: 25px;
            counter-increment: step;
        }
        
        .step::before {
            content: counter(step);
            position: absolute;
            left: 0;
            top: 0;
            width: 40px;
            height: 40px;
            background-color: var(--primary);
            color: var(--white);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }
        
        .step-title {
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        /* Commands */
        .command {
            background-color: var(--dark);
            color: var(--white);
            border-radius: 6px;
            padding: 12px 15px;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .command::before {
            content: "$";
            color: var(--success);
        }
        
        /* Footer */
        footer {
            background-color: var(--dark);
            color: var(--white);
            padding: 60px 0 40px;
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
        }
        
        .footer-column h3 {
            font-size: 1.3rem;
            margin-bottom: 20px;
            color: var(--white);
        }
        
        .footer-links {
            list-style: none;
        }
        
        .footer-links li {
            margin-bottom: 12px;
        }
        
        .footer-links a {
            color: #cbd5e1;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-links a:hover {
            color: var(--accent);
        }
        
        .footer-bottom {
            text-align: center;
            padding-top: 30px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #94a3b8;
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .nav-links {
                display: none;
            }
            
            .screenshots {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-network-wired"></i>
                </div>
                <h1>NetForge</h1>
                <p class="subtitle">Custom TCP/IP Protocol Stack Implementation</p>
                <p class="author">Developed by Yx0R</p>
                <div class="badges">
                    <div class="badge">
                        <i class="fas fa-star"></i> GitHub Stars
                    </div>
                    <div class="badge">
                        <i class="fas fa-code-branch"></i> Forks
                    </div>
                    <div class="badge">
                        <i class="fas fa-certificate"></i> MIT License
                    </div>
                    <div class="badge">
                        <i class="fas fa-code"></i> C Language
                    </div>
                    <div class="badge">
                        <i class="fab fa-linux"></i> Linux
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Navigation -->
    <nav>
        <div class="container">
            <div class="nav-container">
                <div class="nav-logo">NetForge</div>
                <div class="nav-links">
                    <a href="#overview">Overview</a>
                    <a href="#architecture">Architecture</a>
                    <a href="#installation">Installation</a>
                    <a href="#usage">Usage</a>
                    <a href="#screenshots">Screenshots</a>
                    <a href="#contribute">Contribute</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main>
        <div class="container">
            <!-- Overview Section -->
            <section id="overview" class="section">
                <h2 class="section-title">
                    <i class="fas fa-info-circle"></i> Overview
                </h2>
                <div class="section-content">
                    <p><strong>NetForge</strong> is a complete, from-scratch implementation of the TCP/IP protocol stack that creates <strong>real network packets</strong> detectable by professional tools like Wireshark. Unlike theoretical implementations, NetForge sends actual Ethernet frames over the network interface, providing hands-on understanding of networking fundamentals.</p>
                    
                    <div class="features">
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-packet-broadcast"></i>
                            </div>
                            <h3 class="feature-title">Real Packet Generation</h3>
                            <p class="feature-description">Not simulations, actual network traffic</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-search"></i>
                            </div>
                            <h3 class="feature-title">Wireshark Compatible</h3>
                            <p class="feature-description">Professional network analysis</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-layer-group"></i>
                            </div>
                            <h3 class="feature-title">Four-Layer Implementation</h3>
                            <p class="feature-description">Complete TCP/IP model</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-protocol"></i>
                            </div>
                            <h3 class="feature-title">Multiple Protocols</h3>
                            <p class="feature-description">ICMP, TCP, UDP, HTTP, Raw Ethernet</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-graduation-cap"></i>
                            </div>
                            <h3 class="feature-title">Educational Focus</h3>
                            <p class="feature-description">Clear code with extensive documentation</p>
                        </div>
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="fas fa-hammer"></i>
                            </div>
                            <h3 class="feature-title">From Scratch</h3>
                            <p class="feature-description">No high-level networking libraries</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Architecture Section -->
            <section id="architecture" class="section">
                <h2 class="section-title">
                    <i class="fas fa-sitemap"></i> Technical Architecture
                </h2>
                <div class="section-content">
                    <h3>Project Structure</h3>
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">Project Directory</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>netforge/
├── src/
│   ├── main.c              # Application entry point & CLI
│   ├── protocols.h         # Common headers and declarations
│   ├── ipv4.c             # Internet Layer - IPv4 implementation
│   ├── icmp.c             # Transport Layer - ICMP (ping)
│   ├── tcp.c              # Transport Layer - TCP protocol
│   ├── udp.c              # Transport Layer - UDP protocol
│   └── ethernet.c         # Link Layer - Ethernet helpers
├── Makefile               # Build system
└── README.md              # This documentation</pre>
                    </div>
                    
                    <h3>TCP/IP Protocol Stack</h3>
                    <div class="diagram">
                        <div class="diagram-title">Four-Layer TCP/IP Model</div>
                        <div class="protocol-stack">
                            <div class="layer layer-app">
                                <span>Application Layer</span>
                                <span>User data and high-level protocols</span>
                            </div>
                            <div class="layer layer-transport">
                                <span>Transport Layer</span>
                                <span>End-to-end communication (TCP/UDP)</span>
                            </div>
                            <div class="layer layer-internet">
                                <span>Internet Layer</span>
                                <span>Logical addressing and routing (IP)</span>
                            </div>
                            <div class="layer layer-link">
                                <span>Link Layer</span>
                                <span>Physical network interface (Ethernet)</span>
                            </div>
                        </div>
                    </div>
                    
                    <h3>Core Components</h3>
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">Raw Socket Management</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>// Creates low-level socket for direct packet injection
int sock = socket(AF_PACKET, SOCK_RAW, htons(ETH_P_ALL));</pre>
                    </div>
                    
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">Ethernet Frame Structure</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>struct ethhdr {
    unsigned char h_dest[6];   // Destination MAC
    unsigned char h_source[6]; // Source MAC  
    unsigned short h_proto;    // EtherType
};</pre>
                    </div>
                    
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">IP Packet Structure</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>struct iphdr {
    uint8_t  version:4, ihl:4; // Version + Header Length
    uint8_t  tos;              // Type of Service
    uint16_t tot_len;          // Total Length
    uint16_t id;               // Identification
    // ... RFC 791 compliant fields
};</pre>
                    </div>
                </div>
            </section>

            <!-- Installation Section -->
            <section id="installation" class="section">
                <h2 class="section-title">
                    <i class="fas fa-download"></i> Installation & Setup
                </h2>
                <div class="section-content">
                    <h3>Prerequisites</h3>
                    <ul>
                        <li>Linux operating system</li>
                        <li>GCC compiler</li>
                        <li>Root access (for raw sockets)</li>
                        <li>Wireshark (for packet analysis)</li>
                    </ul>
                    
                    <h3>Quick Start</h3>
                    <div class="steps">
                        <div class="step">
                            <div class="step-title">Clone and build</div>
                            <div class="command">git clone &lt;repository&gt;</div>
                            <div class="command">cd netforge</div>
                            <div class="command">make</div>
                        </div>
                        <div class="step">
                            <div class="step-title">Enable raw socket capabilities</div>
                            <div class="command">sudo setcap cap_net_raw+ep netforge</div>
                        </div>
                        <div class="step">
                            <div class="step-title">Find your network interface</div>
                            <div class="command">ip link show</div>
                        </div>
                        <div class="step">
                            <div class="step-title">Start packet capture</div>
                            <div class="command">sudo wireshark</div>
                        </div>
                        <div class="step">
                            <div class="step-title">Send test packets</div>
                            <div class="command">./netforge eth0 ping 8.8.8.8</div>
                        </div>
                    </div>
                    
                    <h3>Advanced Installation</h3>
                    <div class="command">make install</div>
                    <div class="command">make debug</div>
                    <div class="command">make clean</div>
                </div>
            </section>

            <!-- Usage Section -->
            <section id="usage" class="section">
                <h2 class="section-title">
                    <i class="fas fa-terminal"></i> Usage Guide
                </h2>
                <div class="section-content">
                    <h3>Basic Commands</h3>
                    <div class="command">./netforge eth0 info</div>
                    <div class="command">./netforge eth0 ping 8.8.8.8</div>
                    <div class="command">./netforge eth0 tcp 192.168.1.1 80</div>
                    <div class="command">./netforge eth0 udp 192.168.1.1 53</div>
                    <div class="command">./netforge eth0 http 192.168.1.1</div>
                    <div class="command">./netforge eth0 raw</div>
                    <div class="command">./netforge eth0 all 192.168.1.1</div>
                    
                    <h3>Protocol-Specific Examples</h3>
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">ICMP Ping</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>./netforge eth0 ping 8.8.8.8</pre>
                    </div>
                    <p>Creates:</p>
                    <ul>
                        <li>Ethernet frame with broadcast MAC</li>
                        <li>IP packet with TTL=64</li>
                        <li>ICMP Echo Request with sequence number</li>
                        <li>Visible in Wireshark as standard ping</li>
                    </ul>
                    
                    <div class="code-block">
                        <div class="code-header">
                            <div class="code-title">TCP SYN</div>
                            <button class="copy-btn">Copy</button>
                        </div>
                        <pre>./netforge eth0 tcp 192.168.1.1 443</pre>
                    </div>
                    <p>Creates:</p>
                    <ul>
                        <li>TCP segment with SYN flag set</li>
                        <li>Random source port + specified destination port</li>
                        <li>Sequence number based on current time</li>
                        <li>Initiates three-way handshake</li>
                    </ul>
                </div>
            </section>

            <!-- Screenshots Section -->
            <section id="screenshots" class="section">
                <h2 class="section-title">
                    <i class="fas fa-images"></i> Screenshots
                </h2>
                <div class="section-content">
                    <div class="screenshots">
                        <div class="screenshot-card">
                            <img src="https://github.com/user-attachments/assets/4bf50f74-0481-40e3-abf0-ecfb48658298" alt="Usage Instructions" class="screenshot-img">
                            <div class="screenshot-caption">Usage Instructions</div>
                        </div>
                        <div class="screenshot-card">
                            <img src="https://github.com/user-attachments/assets/02651d5e-4901-4327-9526-6b6fffe8418c" alt="Packet Capture on Wireshark" class="screenshot-img">
                            <div class="screenshot-caption">Successful Packet Capture on Wireshark</div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Contribute Section -->
            <section id="contribute" class="section">
                <h2 class="section-title">
                    <i class="fas fa-hands-helping"></i> Contributing
                </h2>
                <div class="section-content">
                    <p>NetForge welcomes contributions! Areas of particular interest:</p>
                    <ul>
                        <li>New Protocol Implementations</li>
                        <li>Performance Optimizations</li>
                        <li>Additional Documentation</li>
                        <li>Testing and Validation</li>
                        <li>Cross-platform Support</li>
                    </ul>
                    
                    <h3>Development Setup</h3>
                    <div class="command">git clone &lt;repository&gt;</div>
                    <div class="command">cd netforge</div>
                    <div class="command">make debug</div>
                    <div class="command">gdb ./netforge</div>
                </div>
            </section>
        </div>
    </main>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>NetForge</h3>
                    <p>A complete, from-scratch implementation of the TCP/IP protocol stack for educational purposes.</p>
                </div>
                <div class="footer-column">
                    <h3>Resources</h3>
                    <ul class="footer-links">
                        <li><a href="#">Documentation</a></li>
                        <li><a href="#">GitHub Repository</a></li>
                        <li><a href="#">RFC Documents</a></li>
                        <li><a href="#">Learning Resources</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Connect</h3>
                    <ul class="footer-links">
                        <li><a href="#">Report Issues</a></li>
                        <li><a href="#">Feature Requests</a></li>
                        <li><a href="#">Discussions</a></li>
                        <li><a href="#">Contact Developer</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Support</h3>
                    <p>If you find NetForge helpful, please consider starring the repository on GitHub or contributing to its development.</p>
                </div>
            </div>
            <div class="footer-bottom">
                <p>&copy; 2023 NetForge. Developed by Yx0R. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <script>
        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });
        
        // Copy code to clipboard
        document.querySelectorAll('.copy-btn').forEach(button => {
            button.addEventListener('click', function() {
                const codeBlock = this.parentElement.nextElementSibling;
                const textArea = document.createElement('textarea');
                textArea.value = codeBlock.textContent;
                document.body.appendChild(textArea);
                textArea.select();
                document.execCommand('copy');
                document.body.removeChild(textArea);
                
                // Change button text temporarily
                const originalText = this.textContent;
                this.textContent = 'Copied!';
                setTimeout(() => {
                    this.textContent = originalText;
                }, 2000);
            });
        });
    </script>
</body>
</html>
