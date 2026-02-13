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

.. tip::

   **The "ClearLagg" Trap**: Avoid plugins that "clear items" or "kill all mobs" to save lag.
   These often cause TPS spikes themselves when they run. Proper configuration in the files
   above is almost always more efficient.

.. seealso::

   * :doc:`troubleshooting`: Learn how to diagnose and fix performance issues using Spark.
   * :doc:`plugin_alternatives`: Find free alternatives to expensive premium plugins.
   * `PaperMC Optimization Guide <https://docs.papermc.io/paper/next-steps/#optimization>`_: The official documentation for performance written by the PaperMC team.


