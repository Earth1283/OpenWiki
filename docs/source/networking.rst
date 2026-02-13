Networking & Proxies
====================

As your community grows, you may find that a single Minecraft server isn't enough. Networking allows you to link multiple servers together, protect your backend IP, and even allow mobile players to join your Java Edition server.

The Proxy: Your Server's Front Door
-----------------------------------

A :term:`proxy` is a specialized server that sits between the player and your actual game servers. Players connect to the proxy, and the proxy "routes" them to the correct sub-server (e.g., Lobby, Survival, Creative).

.. mermaid::

   graph LR
       Player((Player)) -- Connection --> Proxy["Velocity Proxy<br/>(Port: 25565)"]
       
       subgraph Backend_Network [Isolated Backend]
           Proxy -- "Internal Forward" --> Lobby[Lobby Server]
           Proxy -- "Internal Forward" --> Survival[Survival Server]
           Proxy -- "Internal Forward" --> Creative[Creative Server]
       end
       
       style Proxy fill:#eff6ff,stroke:#1e40af,stroke-width:2px,color:#1e40af
       style Backend_Network fill:#f9fafb,stroke:#374151,stroke-dasharray: 5 5

.. tab-set::

   .. tab-item:: 🌌 Velocity
      :sync: velocity

      **The Modern Choice.** Developed by the PaperMC team, Velocity is built for high performance and modern security.
      
      *   **Pros**: Highly efficient, excellent API for developers, native support for modern Minecraft features.
      *   **Modern Forwarding**: Uses `MODERN` forwarding, which is more secure than BungeeCord's `LEGACY` mode. It uses a secret key to ensure that only your proxy can connect to your backend servers.
      *   **Verdict**: **Highly Recommended** for all new networks.

   .. tab-item:: 🦘 BungeeCord / Waterfall
      :sync: bungee

      **The Legacy Standard.** 
      
      *   **Pros**: Massive library of legacy plugins.
      *   **Cons**: Waterfall (the optimized version) is now deprecated in favor of Velocity. BungeeCord itself is slower and lacks many modern optimizations.
      *   **Verdict**: Only use if you have an ancient plugin that *only* works on BungeeCord.

Cross-Platform Play: Java + Bedrock
-----------------------------------

By default, Minecraft: Java Edition and Minecraft: Bedrock Edition (Console, Mobile, Windows 10) cannot play together. `Geyser <https://geysermc.org/>`_ bridges this gap.

*   **Geyser**: A proxy (or plugin) that "translates" Bedrock packets into Java packets in real-time.
*   **Floodgate**: A companion plugin that allows Bedrock players to join without needing a Java Edition account.

.. tip::

   Running Geyser on a **Velocity** proxy is the most stable and efficient way to support Bedrock players on a network.

Velocity Advanced Configuration
-------------------------------

To get the most out of Velocity, you need to tune its `velocity.toml` file.

*   **player-info-forwarding-mode**: Set this to ``modern``. This is the most secure method. You will need to copy the `forwarding.secret` to all your backend Paper/Purpur servers.
*   **compression-level**: The default is fine, but if you have a very high-performance CPU, you can increase this to save bandwidth at the cost of CPU cycles.
*   **haproxy-protocol**: Set this to ``true`` **only** if you are using a load balancer or service like TCPShield that supports the PROXY protocol. This allows the proxy to see the player's real IP instead of the load balancer's IP.

Protecting Your Backend IP
--------------------------

If an attacker discovers your "Backend IP" (the actual IP of your VPS or home PC), they can bypass your proxy's security or target you with DDoS attacks.

1.  **Firewalling**: Configure your game servers to **only** accept connections from your Proxy's IP.
2.  **TCPShield**: (See :doc:`security`) A service that hides your IP behind a protected global network.
3.  **Proxy-Protocol**: Enable this in your proxy and game server settings to ensure player IPs are correctly passed through to your plugins (essential for banning).

Common Networking Pitfalls
--------------------------

*   **"Port 25565 is already in use"**: Only one application can use a port at a time. If you run a Proxy and a Game Server on the same machine, they **must** have different ports (e.g., Proxy on 25565, Lobby on 25566).
*   **IP-Forwarding**: If you don't enable this, every player will appear to have the IP of your Proxy (`127.0.0.1`). This makes banning individuals impossible and breaks security plugins.
*   **Latency (Ping)**: Every "hop" (Player -> Proxy -> Game Server) adds a small amount of latency. Ensure your proxy and game servers are located in the same data center to minimize this.

.. seealso::

   * :doc:`security`: Advanced networking security and DDoS mitigation.
   * `Velocity Documentation <https://docs.papermc.io/velocity>`_: The official guide for setting up your first network.
