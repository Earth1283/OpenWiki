The FOSS Alternative Table
===========================

In the spirit of low-budget server hosting, we prioritize **Free and Open Source Software (FOSS)**. Many high-priced "premium" plugins have open-source counterparts that are equal to—or in some cases, better than—their paid versions.

Below is a mapping of common premium plugins to their FOSS alternatives. 

.. list-table:: Premium vs. FOSS Alternatives
   :widths: 30 30 40
   :header-rows: 1

   * - Category
     - Premium Plugin
     - FOSS Alternative
   * - **Anti-Cheat**
     - `Vulcan <https://www.spigotmc.org/resources/vulcan-advanced-cheat-detection-1-7-1-21.83626/>`_ (Still, use this if you have a budget)
     - `GrimAC <https://github.com/GrimAnticheat/Grim>`_ or `Lightning <https://github.com/Lightning-AntiCheat/Lightning>`_
   * - **All-in-One**
     - `CMI <https://www.spigotmc.org/resources/cmi-270-commands-insane-kit-editor-portals-essentials-economy-mysql-sqlite-much-more.3742/>`_
     - `EssentialsX <https://essentialsx.net/>`_ OR `SunLight <https://github.com/nulli0n/SunLight-spigot>`_
   * - **Backups**
     - `BetterBackups <https://www.spigotmc.org/resources/betterbackups.74100/>`_
     - `DriveBackupV2 <https://github.com/MaxMaeder/DriveBackupV2>`_
   * - **Anti-Bot**
     - `FlameCord <https://www.builtbybit.com/resources/flamecord-fix-lag-and-stop-bot-attacks.13492/>`_
     - `Sonar <https://github.com/flyte-dev/sonar>`_ 
   * - **Land Claiming**
     - `AdvancedRegionMarket <https://www.spigotmc.org/resources/advancedregionmarket.58756/>`_ OR Residence
     - `Dominion <https://github.com/Zrips/Dominion>`_
   * - **Optimization**
     - `ClearLagg <https://dev.bukkit.org/projects/clearlagg>`_ (Note: Don't use this!)
     - None (Use native config tweaks instead)
   * - **Permissions**
     - (Legacy Paid Plugins)
     - `LuckPerms <https://luckperms.net/>`_ (The Industry Standard)
   * - **Homes/TPA/Warp Plugins**
     - Most are free, but they don't have that good of an implementation. For example, EssentialsX, JustTPA, WildRTP...
     - `Huskhomes <https://www.modrinth.com/plugin/huskhomes>`_ - Free and open source, has intutive chat message formatting and so much more.
   * - **Menus/GUI Menus**
     - Your paid GUI plugin, or `DeluxeMenus <https://www.spigotmc.org/resources/deluxemenus.11734/>`_
     - `Zmenus <https://modrinth.com/plugin/>`_, a more modern solution to the older DeluxeMenus plugin. It supports your exsisting DeluxeMenus configurations out of the box.

.. note::

  **A note on "Optimization Plugins":** Many premium plugins claim to "fix lag" by removing entities or clearing items.
  In 99% of cases, these plugins actually **cause** more lag or break vanilla mechanics.
  We recommend using native configuration files such as `paper-world-defaults.yml` or
  `paper-global.yml` instead. They run natively on the server.jar and performs infinitely better
  than any paid plugin that claims to "fix lag" by removing entities.

I need more entries!
-------------------
This table is a work in progress. If you know of a premium (or legacy/old) plugin that has a high-quality and modern FOSS alternative, please let the administrator know or submit a pull request!
