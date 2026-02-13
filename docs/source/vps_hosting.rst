VPS Hosting: The Power User's Guide
====================================

Virtual Private Servers (VPS) offer the highest level of control and performance for Minecraft server administrators. Unlike managed hosting, you are responsible for the entire software stack, which allows for deeper optimization and better resource management.

Managed vs. VPS: Architecture
-----------------------------

Understanding the difference in control is key to choosing the right environment.

.. mermaid::

   graph TD
       User((User)) --> Managed[Managed Hosting]
       User --> VPS[VPS Hosting]
       
       subgraph Managed Architecture
           Managed --> Panel[Web Panel]
           Panel --> Game[Minecraft Instance]
           style Managed fill:#fce4ec,stroke:#880e4f,stroke-width:2px,color:#880e4f
       end
       
       subgraph VPS Architecture
           VPS --> SSH[SSH / Root Access]
           SSH --> OS[Full Linux OS]
           OS --> Docker[Docker / Panels]
           Docker --> Instance1[Instance 1]
           Docker --> Instance2[Instance 2]
           style VPS fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#01579b
       end

MCSManager: The Modern Panel
---------------------------

`MCSManager <https://mcsmanager.com/>`_ is a lightweight, open-source control panel designed for distributed management. It separates the "Panel" (the web interface) from the "Daemon" (the part that runs the servers).

.. mermaid::

   graph LR
       User((User)) --> Panel[MCSManager Panel]
       Panel -- Network --> Daemon1[Daemon A]
       Panel -- Network --> Daemon2[Daemon B]
       Daemon1 --> S1[Server 1]
       Daemon1 --> S2[Server 2]
       Daemon2 --> S3[Server 3]

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
