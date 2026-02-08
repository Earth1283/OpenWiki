Networking & Proxies
====================

As your community grows, you may find that a single Minecraft server isn't enough. Networking allows you to link multiple servers together, protect your backend IP, and even allow mobile players to join your Java Edition server.

The Proxy: Your Server's Front Door
-----------------------------------

A :term:`proxy` is a specialized server that sits between the player and your actual game servers. Players connect to the proxy, and the proxy "routes" them to the correct sub-server (e.g., Lobby, Survival, Creative).

.. tab-set::

   .. tab-item:: 🌌 Velocity
      :sync: velocity

      **The Modern Choice.** Developed by the PaperMC team, Velocity is built for high performance and modern security.
      
      *   **Pros**: Highly efficient, excellent API for developers, native support for modern Minecraft features.
      *   **Cons**: Requires a slightly different setup for permissions and plugins than older proxies.
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
