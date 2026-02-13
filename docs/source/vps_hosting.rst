VPS Hosting: The Power User's Guide
====================================

Virtual Private Servers (VPS) offer the highest level of control and performance for Minecraft server administrators. Unlike managed hosting, you are responsible for the entire software stack, which allows for deeper optimization and better resource management.

Managed vs. VPS: Architecture
-----------------------------

Understanding the difference in control is key to choosing the right environment.

.. mermaid::

   graph LR
       User((User)) -- Web Access --> Managed["Managed Hosting<br/>(Shared Node)"]
       User -- SSH Access --> VPS["VPS Hosting<br/>(Dedicated OS)"]
       
       subgraph Managed_Env [Managed Environment]
           Managed -- Management --> Panel[Web Control Panel]
           Panel -- Process --> Game[Minecraft Instance]
       end
       
       subgraph VPS_Env [VPS Environment]
           VPS -- Root Access --> OS[Full Linux OS]
           OS -- Containerization --> Docker[Docker / Panels]
           Docker -- Isolation --> Instance1[Instance 1]
           Docker -- Isolation --> Instance2[Instance 2]
       end
       
       style Managed_Env fill:#fdf2f2,stroke:#9b1c1c,stroke-dasharray: 5 5
       style VPS_Env fill:#f0f9ff,stroke:#075985,stroke-dasharray: 5 5
       style Panel fill:#fdf2f2,stroke:#9b1c1c,color:#9b1c1c
       style OS fill:#f0f9ff,stroke:#075985,color:#075985

MCSManager: The Modern Panel
---------------------------

`MCSManager <https://mcsmanager.com/>`_ is a lightweight, open-source control panel designed for distributed management. It separates the "Panel" (the web interface) from the "Daemon" (the part that runs the servers).

.. mermaid::

   graph LR
       User((User)) -- HTTPS --> Panel["MCSManager Panel<br/>(Web Interface)"]
       
       subgraph Remote_Nodes [Distributed Daemons]
           Panel -- "Secure Network" --> Daemon1[Daemon A]
           Panel -- "Secure Network" --> Daemon2[Daemon B]
           Daemon1 -- Process --> S1[Server 1]
           Daemon1 -- Process --> S2[Server 2]
           Daemon2 -- Process --> S3[Server 3]
       end
       
       style Remote_Nodes fill:#f9fafb,stroke:#374151,stroke-dasharray: 5 5
       style Panel fill:#eff6ff,stroke:#1e40af,color:#1e40af
       style Daemon1 fill:#ecfdf5,stroke:#065f46,color:#065f46
       style Daemon2 fill:#ecfdf5,stroke:#065f46,color:#065f46

Setup Guide
~~~~~~~~~~~

1.  **Preparation**: Ensure you have a clean install of Ubuntu 22.04 or 24.04.
2.  **One-Line Install**:
    .. code-block:: bash

       wget -qO- https://github.com/MCSManager/MCSManager/releases/latest/download/install_en.sh | bash
3.  **Access**: Once installed, visit ``http://your-ip:23333``.
4.  **Create an Instance**:
    *   Navigate to **Instances** -> **Create Instance**.
    *   Select **Minecraft** -> **Java Edition**.
    *   Choose **Docker** as the runtime (highly recommended for isolation).
    *   Upload your `server.jar` and click **Start**.

Domain Configuration
--------------------

Connecting a domain to your VPS involves setting up DNS records.

.. mermaid::

   sequenceDiagram
       participant Player
       participant CF as DNS Provider (e.g. Cloudflare)
       participant VPS as VPS Server
       
       Player->>CF: Resolve play.example.com
       CF-->>Player: Return VPS IP (e.g. 1.2.3.4)
       Player->>VPS: Connect to 1.2.3.4:25565

Pointing an A-Record
~~~~~~~~~~~~~~~~~~~~

1.  Log into your domain registrar (Namecheap, Cloudflare, etc.).
2.  Go to the **DNS Management** section.
3.  Add an **A Record**:
    *   **Name**: ``play`` (or ``@`` for the root domain).
    *   **Value**: Your VPS IPv4 address.
    *   **TTL**: Auto or 3600.
4.  Players can now join using ``play.yourdomain.com``.

Cloudflare: DNS vs. Proxy
~~~~~~~~~~~~~~~~~~~~~~~~~

If you use Cloudflare, you will see a toggle for the "Orange Cloud" (Proxy).

*   **DNS Only (Grey Cloud)**: **REQUIRED** for Minecraft. Minecraft uses a protocol that Cloudflare's standard proxy does not support. If you turn on the orange cloud, players will not be able to connect unless you use **Cloudflare Spectrum** (paid) or a third-party service like **TCPShield**.
*   **DNS Proxy (Orange Cloud)**: Only for web-based services (like your MCSManager panel).

Dos and Don'ts
--------------

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - ✅ DO
     - ❌ DON'T
   * - Use **SSH Keys** for authentication.
     - Never use simple passwords for root.
   * - Run servers as a **non-root user**.
     - Don't run `java -jar` directly as root.
   * - Use **Docker** for instance isolation.
     - Don't mix multiple servers in one folder.
   * - Configure a **Firewall (UFW)**.
     - Don't leave unused ports open.
   * - Set up **Off-site Backups**.
     - Don't store backups on the same disk.

Where to Find Reliable VPS Hosting
----------------------------------

.. grid:: 1 2 2 2
   :gutter: 3

   .. grid-item-card:: 🔎 Deal Hunting
      :class-header: sd-bg-info sd-text-white

      *   `LowEndTalk <https://lowendtalk.com/>`_: Best for limited-time aggressive deals.
      *   `LowEndBox <https://lowendbox.com/>`_: Curated budget-friendly VPS offers.

   .. grid-item-card:: 🌐 Established Providers
      :class-header: sd-bg-success sd-text-white

      *   `Hetzner <https://www.hetzner.com/>`_: European gold standard for price/performance.
      *   `BuyVM <https://buyvm.net/>`_: Known for DDoS protection and storage "Slabs".

   .. grid-item-card:: ☁️ Cloud Giants
      :class-header: sd-bg-primary sd-text-white

      *   `Oracle Cloud <https://www.oracle.com/cloud/free/>`_: Amazing "Always Free" ARM tier (24GB RAM).
      *   `Akamai <https://www.linode.com/>`_: Reliable, high-quality support and networking.
