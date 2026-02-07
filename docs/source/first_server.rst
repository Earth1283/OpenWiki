Creating Your First Server
==========================

.. _installation:

Picking Your Server Software
----------------------------

There are many open and closed sourced Minecraft server software available 
for you to choose from that many do not know which to choose. For instance,
there is the obvious choice of `PaperMC <https://papermc.io/downloads/paper>`_,
and the newer options of "performance forks" (we will cover that in a moment)
such as `LeafMC <https://www.leafmc.one/downloads>`_.

Minecraft server software has come a long way since the early 2010s. It went like this:

.. mermaid::

    graph TD
        %% Nodes
        Vanilla[Vanilla - Mojang Official]
        hMod[hMod - Legacy Wrapper]
        CraftBukkit[CraftBukkit - The API Foundation]
        Spigot[Spigot - Performance & Anti-Xray]
        Paper[PaperMC - The Industry Standard]
        Tuinity[Tuinity - Optimized Logic/Starlight]
        Pufferfish[Pufferfish - Enterprise Performance]
        Purpur[PurpurMC - Feature-Rich Customization]
        Leaf[Leaf - Extreme Performance / Unstable]

        %% Evolution Flow
        Vanilla --> hMod
        Vanilla --> CraftBukkit
        hMod -.->|Team Transition| CraftBukkit
        CraftBukkit --> Spigot
        Spigot --> Paper
        Paper --> Tuinity
        Tuinity -->|Merged into| Paper
        Paper --> Pufferfish
        Pufferfish --> Purpur
        Purpur --> Leaf

        %% Styling
        style Vanilla fill:#f9f,stroke:#333,stroke-width:2px
        style Paper fill:#00d2ff,stroke:#000,stroke-width:2px
        style Purpur fill:#b19cd9,stroke:#000,stroke-width:2px
        style Leaf fill:#ff6666,stroke:#800,stroke-width:3px,stroke-dasharray: 5 5

As you can see, the "evolution" of server forks in the past decade or so
has been blazingly fast. This started from the vanilla server.jar, which is
distributed by Mojang. It is **not advised** for you to use this. Similarly,
old and discontinued forks such as (CraftBukkit) Bukkit are not advised.

At a bare minimum, you should use PaperMC, or, if you feel like using a more configurable
server version, choose PurpurMC. These are the two forks that are regarded as "most stable"
for modern Minecraft.

.. warning ::
    Unless your hardware is **heavily constrained**, do NOT use Leaf. It is
    not worth running the risk of potential playerdata corruption for performance that
    has yet to proven its stability.

As a good rule of thumb, always fetch the latest release from the respective source.
There is absolutely no point in, say, fetching release 123 when release 132 is available.
New releases often fix security vulnerabilities and duplication glitches/exploits which older
builds do not cover.

.. tip::
    If you are running a server with a version number higher than `1.9.2`, the server
    would typically make an `eula.txt` file for you to set `eula=false` to `eula=true`.
    
    In order to automate this process (especially if you are on a bare metal VPS), it is
    best if you can run the following command:

    .. tabs::

       .. tab:: Linux / macOS

          .. code-block:: bash

             rm eula.txt; echo "eula=true" > eula.txt

       .. tab:: Windows (PowerShell)

          .. code-block:: powershell

             Remove-Item eula.txt; "eula=true" | Out-File eula.txt -Encoding ascii

    This command removes the original eula.txt (in case there was some hanging data), and
    the second part of the command creates a new one with the correct value.

The following sections will explore the nuances of certain server software.

.. tab-set::

   .. tab-item:: PaperMC
      :sync: paper

      **PaperMC** is the industry standard for reliability and stability. 
      
      * **Pros**: Highly stable, consistent gameplay, excellent anti-xray.
      * **Cons**: Conservative regarding new feature requests.

   .. tab-item:: PurpurMC
      :sync: purpur

      **PurpurMC** is for those who want ultimate control.
      
      * **Pros**: Thousands of configuration options, downstream of Pufferfish/Paper.
      * **Cons**: Can be overwhelming for beginners.

.. sidebar:: Software Choice at a Glance

   * **Stability**: PaperMC
   * **Customization**: PurpurMC
   * **Experimental**: LeafMC
   * **Avoid**: Vanilla, CraftBukkit

Pros and Cons of PaperMC
------------------------
PaperMC, as the industry standard for so many years, is known for its reliability, stability, and performance
compared to previous implementations/versions of the Spigot/Bukkit API. PaperMC tries to implement
vanilla features while maximizing performance.

PaperMC in itself is very configurable, allowing you access to Bukkit, Spigot, and Paper's configuration
files. You can tweak mob spawn times, item despawn times, and even configure one of the
best and most performant anti-xray features on planet Earth.

The obvious disadvantage of PaperMC is that their core development team believes that PaperMC
should remain as closely vanilla-ish as possible, often rejecting creative options that PurpurMC accepts.

Pros and Cons of PurpurMC
-------------------------
PurpurMC, as a :term:`fork` of Pufferfish (in turn, a :term:`fork` of Paper), offers more optimizations and creative configuration options
when compared to traditional Paper. Purpur is famous for their `purpur.yml` that is, though thousands of lines long,
offers more configurability than any amount of default PaperMC configurations could offer.

Purpur, being a downstream :term:`fork` from Pufferfish, benefits from Pufferfish's optimizations, which compounds
towards their further optimizations in purpur.yml.

The downside is clear. PurpurMC traded configurability with ease of use. People get scared off by Purpur's
thousand-line long `purpur.yml` without deriving its complete value, resulting in an ultimate loss
of potential features presented by Purpur.

.. seealso::

   For a deep dive into squeezing every bit of performance out of your software, check the :doc:`optimization` section.

Setting up your first server
----------------------------
.. warning::
    This guide assumes that you have access to the :term:`JVM` flags of your instance. If you are unable
    to edit them yourself, you should ask your server hosting provider via a ticket. Legitimate hosts
    typically allow these requests, while summer hosts that oversell their nodes typically deny such requests,
    as these flags make the :term:`JVM` allocate memory more efficiently. More on this at a later date.

Begin with downloading the server binary (aka, server.jar) from your vendor, be it Paper or Purpur.

Then place it inside your server directory, and then create a file named `eula.txt` with the following content:

.. code-block:: text

    eula=true

This agrees to the Mojang EULA before the server starts. Then, configure your startup flags.
If you are on a bare metal VPS, do **NOT** allocate all your available memory to the Java :term:`Heap`. This will
lead to your operating system running out of memory and your server crashing.
It is best for you, in this case, to allocate memory with the following function:

.. math::

   RAM_{physical}-2GB=RAM_{allocated}

This provides the :term:`JVM` with enough headroom to store non-heap objects, for Linux to breathe, and for other background processes.

Let's prepare startup flags! Java, unlike C/C++, has a :term:`Garbage Collector (GC)`. To avoid complicating things,
I will simply define it as "something that cleans up unused memory". The default :term:`Garbage Collector` is decent,
though with Minecraft, it is not that ideal. So we need better flags.

.. important::

   Always use **Aikar's Flags** for any server with more than 4GB of RAM. They are specifically tuned to reduce
   "stop-the-world" pauses.

Luckily, Aikar has come to the rescue with his flags. You can check his flags out on
`flags.sh <https://www.flags.sh>`_. These flags aim to improve the performance of the :term:`JVM` and its :term:`Garbage
Collector` aside from the main game. But be wary that this is not a "set and forget" value that you can
set once and forget. More optimization effort will have to be put into the main server configurations to 
truly improve performance.

Understanding the File Structure
--------------------------------
Once you start your server for the first time, you will notice a plethora of files and folders being created.
Understanding these is crucial for effective administration:

world/, world_nether/, world_the_end/
    These folders contain your map data, player statistics, and inventory data.
    **Never** delete these unless you want a full world reset.

plugins/
    This is where you will place your `.jar` plugin files to extend server functionality.

logs/
    Contains historical records of everything that happened in the server console. Useful for debugging crashes.

server.properties
    The main configuration file for vanilla Minecraft settings.

bukkit.yml, spigot.yml, paper-global.yml
    Configuration files for the respective server software layers.

Essential Configuration
-----------------------
The most important file to start with is `server.properties`. Here are a few keys you should look at:

.. table:: Recommended Basic Settings
   :widths: 25 25 50

   ================ ================= ========================================================
   Property         Default           Description
   ================ ================= ========================================================
   server-port      25565             The port players use to connect.
   view-distance    10                How many chunks are sent to the player.
   online-mode      true              Whether to verify accounts with Mojang.
   white-list       false             If true, only whitelisted players can join.
   ================ ================= ========================================================

For performance, you should also look into `paper-world-configuration.yml` (in modern Paper versions)
to tweak entity activation ranges and hopper speeds.


Connecting to Your Server
-------------------------
To join your server, you need an IP address.

1.  **Local Connection**: If the server is running on the same computer you are playing on, use `localhost` or `127.0.0.1`.
2.  **Home Network**: If the server is on a different computer in your house, find its local IP (e.g., `192.168.1.50`).
3.  **Public Access**: To let friends join from outside your house, you must **Port Forward** port `25565` (TCP/UDP) on your router.
    *   *Warning*: Never share your public IP address publicly. Use a domain or a proxy if possible.

Basic Server Commands
---------------------
Once you are in-game or using the console, these commands are your best friends:

*   `/op <player>`: Grants a player administrative privileges. Use this sparingly!
*   `/stop`: Safely saves the world and shuts down the server. Always use this instead of just closing the window.
*   `/save-all`: Forces a world save immediately.
*   `/whitelist on/off`: Enables or disables the whitelist.
*   `/whitelist add <player>`: Allows a specific player to join when the whitelist is active.

Introduction to Plugins
-----------------------
Plugins allow you to add features like teleports (`/tp`), economy systems, and land protection.

**Where to find plugins:**
*   `Hangar <https://hangar.papermc.io/>`_: The official PaperMC plugin repository.
*   `Modrinth <https://modrinth.com/plugins>`_: A modern, fast, and open-source platform for plugins and mods.
*   `SpigotMC <https://www.spigotmc.org/resources/>`_: The classic destination for thousands of plugins.

**How to install:**
1.  Download the `.jar` file.
2.  Drop it into the `plugins/` folder.
3.  Restart the server or use a plugin loader (though a full restart is always safer).

Avoid "leaked" or "cracked" plugin sites at all costs, as they often contain malware that can
backdoor your server or steal your data.