Creating Your First Server: The Master Guide
===========================================

.. _installation:

Setting up a Minecraft server is a rite of passage for many, but doing it **right** requires a deep understanding of the underlying technology. This guide is designed to be the most comprehensive resource available for starting your journey as a server administrator.

Phase 1: Preparing Your Environment
-----------------------------------
Before downloading a single file, you must prepare your operating system. Minecraft is a Java-based application, and its performance depends heavily on the environment it runs in.

.. tab-set::

   .. tab-item:: 🪟 Windows
      :sync: win

      1. **Install Java**: Download the **x64 MSI Installer** for Java 21 from `Adoptium <https://adoptium.net/temurin/releases/?version=21>`_.
      2. **Environment Variables**: 
         * Search for "Edit the system environment variables" in your start menu.
         * Click "Environment Variables".
         * Under "System variables", ensure ``JAVA_HOME`` points to your installation path.
      3. **Show File Extensions**: In File Explorer, go to View > Show > **File name extensions**. This is critical for creating start scripts.

   .. tab-item:: 🐧 Linux (Ubuntu/Debian)
      :sync: linux

      1. **Update Repositories**:
         .. code-block:: bash

            sudo apt update && sudo apt upgrade -y
      2. **Install Java 21**:
         .. code-block:: bash

            sudo apt install openjdk-21-jre-headless -y
      3. **Create a User**: **Never** run your server as root.
         .. code-block:: bash

            sudo adduser minecraft
            su - minecraft

   .. tab-item:: 🍎 macOS
      :sync: mac

      1. **Install Homebrew**: (Recommended) 
         .. code-block:: bash

            /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
      2. **Install Java**:
         .. code-block:: bash

            brew install openjdk@21
      3. **Pathing**: Follow the instructions provided by brew to symlink the openjdk folder so the system can find it.

Phase 2: Choosing Your Software Layer
-------------------------------------
The "flavor" of server software you choose determines which plugins you can run and how much performance you can squeeze out of your hardware.

.. tab-set::

   .. tab-item:: 📜 `Spigot <https://www.spigotmc.org/>`_
      :sync: spigot

      The successor to Bukkit. It introduced "BuildTools" and early performance patches.
      
      * **Pros**: High plugin compatibility.
      * **Cons**: Slower updates, lacks modern optimizations like Starlight or Lithium.
      * **Verdict**: Legacy. Only use if a specific plugin *requires* it.

   .. tab-item:: 📄 `PaperMC <https://papermc.io/>`_
      :sync: paper

      The industry standard. It is a :term:`fork` of Spigot that fixes gameplay inconsistencies and massive performance holes.
      
      * **Pros**: Async chunk loading, exploit fixes, active development.
      * **Cons**: Some technical "vanilla" redstone machines may behave differently.
      * **Verdict**: **Recommended** for 90% of all servers.

   .. tab-item:: 🪵 `PurpurMC <https://purpurmc.org/>`_
      :sync: purpur

      A :term:`fork` of Paper (via Pufferfish) that adds hundreds of "fun" configuration toggles.
      
      * **Pros**: Ridable mobs, customizable villager behavior, extreme performance tweaks.
      * **Cons**: Can be complex to configure perfectly.
      * **Verdict**: The choice for power users who want maximum customization.

Phase 3: Deep Dive into Configuration
-------------------------------------
Your `server.properties` file is the brain of your server. Let's break it down into granular categories.

.. tab-set::

   .. tab-item:: 🎮 Gameplay Settings
      :sync: gameplay

      * ``gamemode``: Sets the default mode (survival, creative, etc.).
      * ``difficulty``: We recommend ``hard`` for better mob spawn rates and meaningful gameplay.
      * ``pvp``: Enable or disable player-vs-player combat globally.
      * ``allow-flight``: Set to ``true`` only if you have plugins that allow flying, otherwise the server will kick players for "floating too long."

   .. tab-item:: ⚙️ Performance Settings
      :sync: performance

      * ``view-distance``: Controls chunk rendering. **8** is the sweet spot for survival.
      * ``simulation-distance``: Controls entity ticking. **5-6** is recommended to save CPU.
      * ``network-compression-threshold``: **256**. Lowering this increases CPU usage; raising it increases bandwidth usage.
      * ``max-tick-time``: **60000**. This prevents the server from crashing if a single tick takes too long (common during backups).

   .. tab-item:: 🔒 Security Settings
      :sync: security

      * ``online-mode``: **MUST BE TRUE**. Setting this to false allows anyone to join as anyone else (impersonation).
      * ``enable-query``: Set to ``false`` unless you use a server list that requires it.
      * ``hide-online-players``: If true, players won't see who is online in the server list (good for privacy).

Phase 4: Advanced Startup and JVM Tuning
----------------------------------------
How you start your server is just as important as the software itself. Using raw `java -jar` is a recipe for stuttering.

.. tab-set::

   .. tab-item:: 🚀 Aikar's Flags (Standard)
      :sync: aikar

      Recommended for almost everyone. These flags optimize the :term:`Garbage Collector (GC)` to prevent "Lag Spikes".
      
      .. code-block:: bash

         java -Xms4G -Xmx4G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 ... (see optimization page)

   .. tab-item:: 🏎️ ZGC (Experimental)
      :sync: zgc

      If you are using **Java 21** and have more than 12GB of RAM, you can try the Z Garbage Collector.
      
      .. code-block:: bash

         java -Xms12G -Xmx12G -XX:+UseZGC -XX:+ZGenerational -jar server.jar --nogui

      * **Pros**: Ultra-low pause times (usually under 1ms).
      * **Cons**: Higher CPU overhead than G1GC.

Phase 5: Networking & Access
----------------------------
How do players actually get into your world?

.. tab-set::

   .. tab-item:: 🏠 Home Hosting
      :sync: home

      1. **Static IP**: Ensure your server PC has a static local IP (e.g., 192.168.1.10).
      2. **Port Forwarding**: Log into your router (usually 192.168.1.1) and forward **25565 TCP/UDP** to your server PC.
      3. **Dynamic DNS**: Since your home IP changes, use a service like `No-IP <https://www.noip.com/>`_ to get a domain name (e.g., ``mycoolserver.ddns.net``).

   .. tab-item:: ☁️ VPS Hosting
      :sync: vps

      1. **Firewall (UFW)**: 
         .. code-block:: bash

            sudo ufw allow 25565/tcp
            sudo ufw allow 22/tcp (Don't lock yourself out of SSH!)
            sudo ufw enable
      2. **Dedicated IP**: Your VPS usually comes with a static IPv4. You can point a domain A-Record directly to it.

Phase 6: Maintenance & The Long Run
-----------------------------------
A server is not a "set and forget" project. It requires consistent care.

.. tab-set::

   .. tab-item:: 💾 Backup Strategy
      :sync: maintenance

      * **Hot Backups**: Use a plugin while the server is running.
      * **Cold Backups**: Stop the server, zip the entire folder, and move it to a different drive.
      * **Rule of Three**: 3 copies, 2 different formats, 1 off-site.

   .. tab-item:: 🔄 Updating
      :sync: maintenance

      1. Stop the server.
      2. Back up everything.
      3. Replace the `server.jar` with the new version.
      4. Start and check logs for plugin errors.

   .. tab-item:: 📈 Monitoring
      :sync: maintenance

      * **Timings/Spark**: Use `Spark <https://spark.lucko.me/>`_ by running ``/spark profiler`` to see exactly which plugin or entity is causing lag.
      * **TPS**: Monitor your Ticks Per Second. If it's below 20.0, you have work to do.

.. seealso::

   * :doc:`optimization`: The next step in your journey.
   * :doc:`security`: Protecting your community.
   * :doc:`summer_hosts`: Choosing a place to host your masterwork.