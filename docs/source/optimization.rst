Server Optimization
===================

Optimization is a never-ending journey for any Minecraft server administrator.
While modern forks like Paper and Purpur provide a great baseline, you must
tune your configuration to match your hardware and player count.

The Gold Standard Guide
-----------------------
Before tweaking individual values, it is highly recommended to read the
`Minecraft Optimization Guide by YouHaveTrouble <https://github.com/YouHaveTrouble/minecraft-optimization>`_.
This community-maintained guide is the most comprehensive resource for performance tuning.

Key Performance Concepts
------------------------

To optimize a server, you must first understand the **Tick Loop**. A Minecraft server aims to run 20 ticks per second (TPS), meaning each tick has exactly 50ms to complete.

.. mermaid::

   graph TD
       Start((Tick Start)) -- Packets --> Input[Process Network Packets]
       Input -- AI Logic --> AI[Entity AI & Logic]
       AI -- Calculation --> Physics[World Physics & Blocks]
       Physics -- I/O Sync --> Save[Autosave / Disk IO]
       Save -- Response --> Output[Send Packets to Players]
       Output -- Cycle --> End((Tick End))
       
       style Save fill:#fff7ed,stroke:#9a3412,stroke-width:2px,color:#9a3412
       style Start fill:#f0fdf4,stroke:#166534,color:#166534
       style End fill:#fef2f2,stroke:#991b1b,color:#991b1b

Entity Activation Range
~~~~~~~~~~~~~~~~~~~~~~~
Found in `spigot.yml`, this setting controls how close a player must be to an entity (mob, animal, etc.) for it to start :term:`ticking`.

.. tip::

   Lowering these values can significantly reduce CPU usage in areas with many automated farms.

View Distance vs. Simulation Distance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In modern Minecraft (1.18+), these are split into two settings:

*   **View Distance**: How far the player can *see* chunks.
*   **Simulation Distance**: How far from the player the game actually *processes* events (crops growing, redstone, mob AI).

**Recommendation**: Keep Simulation Distance at `4` or `5` for high-performance servers, while View Distance can be slightly higher (e.g., `6-8`) if your network bandwidth allows.

.. hint::

   If you use a :term:`fork` like Purpur, you can even configure these per-world to save resources in less important dimensions.

Network Optimizations
----------------------
Minecraft is a "chatty" protocol. You can optimize the way data is sent to players:

*   **Use a Proxy**: If you have multiple servers, using `Velocity <https://papermc.io/software/velocity>`_ can handle player connections more efficiently than the game server itself.
*   **TCP Fast Open**: If your OS supports it, enabling this can reduce connection latency.

Pre-generating Your World
-------------------------
The most common cause of lag spikes on new servers is chunk generation. When a player explores new territory, the CPU has to work overtime to generate the terrain.

.. error::

   Generating chunks while players are online is the #1 killer of :term:`Ticking` performance.

**The Solution**: Use a plugin like `Chunky <https://modrinth.com/plugin/chunky>`_ to pre-generate your world in a set radius (e.g., 5,000 to 10,000 blocks).

.. code-block:: bash

    /chunky center 0 0
    /chunky radius 5000
    /chunky start

Hardware Considerations
-----------------------
Minecraft is primarily a **single-threaded** application (except Folia).
This means that having 64 cores won't help you as much as having 4 very fast cores.

.. grid:: 1 2 3 3
   :gutter: 2

   .. grid-item-card:: 🧠 CPU
      :class-header: sd-bg-primary sd-text-white

      High single-core clock speed is king.
      ^^^
      Ryzen 7000+ or Intel 13th Gen+ are currently the top performers for Minecraft.

   .. grid-item-card:: 🧊 RAM
      :class-header: sd-bg-success sd-text-white

      Quality over quantity.
      ^^^
      Allocate enough for your :term:`Heap` and leave 2-4GB for the OS and non-heap objects. DDR4/DDR5 recommended.

   .. grid-item-card:: 💽 Storage
      :class-header: sd-bg-info sd-text-white

      NVMe is non-negotiable.
      ^^^
      Standard SSDs are okay, but NVMe prevents stuttering during heavy autosave operations.

Advanced Configuration Deep Dive
--------------------------------

While pre-generation is the most important step, fine-tuning your configuration files allows you to handle more players with less lag.

.. tab-set::

   .. tab-item:: 📄 paper-world-defaults.yml

      Located in `config/paper-world-defaults.yml` (1.19+).

      *   ``max-auto-save-chunks-per-tick``: Set to **6**. This spreads the load of saving world data.
      *   ``prevent-moving-into-unloaded-chunks``: Set to **true**. Prevents players from causing lag by flying into the void.
      *   ``container-update-tick-rate``: Set to **2** or **3**. Slows down how often chests/hoppers update their inventory visuals.
      *   ``mob-effects.undead-immune-to-item-replenishable-effects``: Set to **true**.

   .. tab-item:: 📜 spigot.yml

      *   ``save-user-cache-on-stop-only``: Set to **true**. Reduces disk IO during gameplay.
      *   ``merge-radius``:
          *   ``item``: **4.0**
          *   ``exp``: **6.0**
          (Groups items on the ground to reduce entity count, removing the need for plugins like "Clumps")
      *   ``entity-activation-range``:
          *   ``animals``: **16**
          *   ``monsters``: **24**
          *   ``raiders``: **48**

   .. tab-item:: 🪵 bukkit.yml

      *   ``spawn-limits``:
          *   ``monsters``: **50** (Vanilla is 70; 50 is unnoticeable for most players).
          *   ``animals``: **8**
          *   ``water-animals``: **3**
      *   ``ticks-per``:
          *   ``animal-spawns``: **400** (Spawns animals every 20 seconds instead of every tick).
          *   ``monster-spawns``: **10** (Spawns monsters every 0.5 seconds).

   .. tab-item:: 🚀 purpur.yml

      Located in `purpur.yml`. These are extreme optimizations for power users.

      *   ``villager.lobotomize.enabled``: Set to **true**. Stops villagers from pathfinding unless they are hit or interacted with. Massive CPU saver in trading halls.
      *   ``entities.alternative-item-despawn-rate``: Set to **true**. Allows items to despawn faster if there are too many on the ground.
      *   ``settings.use-alternate-keep-alive``: Set to **true**. Prevents players with bad connections from being timed out as easily.

.. tip::

   **The "ClearLagg" Trap**: Avoid plugins that "clear items" or "kill all mobs" to save lag.
   These often cause TPS spikes themselves when they run. Proper configuration in the files
   above is almost always more efficient.

The Spark Profiler: Identifying the Bottleneck
----------------------------------------------

When your server is lagging (TPS < 20), you need to know *why*. `Spark <https://spark.lucko.me/>`_ is the definitive tool for this.

How to Read a Spark Report
~~~~~~~~~~~~~~~~~~~~~~~~~~

After running ``/spark profiler start`` and generating a link, open the **Viewer**.

1.  **Self Time vs. Total Time**: 
    *   **Total Time**: How much time a function *and everything it called* took.
    *   **Self Time**: How much time *only* that specific function took. Look for high "Self Time" to find the actual source of lag.
2.  **The Tick Loop**: This is the heart of the server. 
    *   If ``Server Hang Watchdog`` is high, the server is freezing.
    *   If ``world - doTick`` is high, the issue is likely entities (mobs) or block updates (redstone).
    *   If a plugin name (e.g., `LuckPerms` or `Essentials`) appears with a high percentage, that plugin is performing poorly.

.. dropdown:: 🕵️ Advanced Spark Analysis

   *   **Garbage Collection (GC)**: If you see frequent spikes in "GC Time," your Java flags are likely poorly configured, or you have too little/too much RAM allocated.
   *   **Scheduled Tasks**: Look for plugins running expensive tasks on the "Main Thread." High-quality plugins will run these "Asynchronously" (off-thread).

JVM Tuning: Why Aikar's Flags?
------------------------------

You will often see administrators recommending a specific set of Java flags. These aren't magic; they are designed to optimize the **G1 Garbage Collector**.

.. mermaid::

   graph LR
       subgraph Physical_RAM [Total Physical RAM]
           direction TB
           OS["Operating System<br/>(2-4GB Reserved)"]
           
           subgraph JVM_Process [Java Virtual Machine]
               Heap["Java Heap Space<br/>(-Xmx / -Xms)"]
               NonHeap["Non-Heap Memory<br/>(Metaspace / Code Cache)"]
           end
       end
       
       style Heap fill:#eff6ff,stroke:#1e40af,color:#1e40af
       style OS fill:#f9fafb,stroke:#374151,color:#374151
       style JVM_Process fill:#f0fdf4,stroke:#166534,stroke-dasharray: 5 5
       style Physical_RAM fill:#ffffff,stroke:#1f2937,stroke-width:2px

*   **-Xmx and -Xms**: Always set these to the same value. This prevents the JVM from constantly resizing its memory pool, which causes lag.
*   **G1GC**: This collector splits the memory into regions, making it much more efficient at cleaning up "trash" without freezing the game.
*   **ZGC (Java 21+)**: The future of Minecraft hosting. It offers sub-millisecond pause times, but requires more CPU power. Only use if you have a modern CPU (Ryzen 7000+ / Intel 13th Gen+).

.. seealso::

   * :doc:`troubleshooting`: Learn how to diagnose and fix performance issues using Spark.
   * :doc:`plugin_alternatives`: Find free alternatives to expensive premium plugins.
   * `PaperMC Optimization Guide <https://docs.papermc.io/paper/next-steps/#optimization>`_: The official documentation for performance written by the PaperMC team.


