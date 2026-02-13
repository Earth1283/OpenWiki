Plugin Selection & Evaluation
=============================

Plugins are the lifeblood of any Minecraft server, but they are also
the most common cause of instability, lag, and security vulnerabilities.
This guide will teach you how to navigate the ecosystem, find high-quality software,
and determine when a "premium" price tag is actually justified.

Where to Look for Plugins
-------------------------

Not all plugin repositories are created equal. Where you download your software
often dictates its quality, safety, and how easy it is to update.

.. tab-set::

   .. tab-item:: 🟢 Modrinth
      :sync: modrinth

      **The Gold Standard for Modern Servers.**
      Modrinth was built from the ground up to solve the problems of older platforms. 

      *   **Safety First**: Every file is scanned for malware, and the platform encourages Open Source (FOSS) development.
      *   **Better Search**: You can filter by "Server Side" to ensure you aren't accidentally downloading client-only mods.
      *   **Technically Superior**: Modrinth uses modern hashing and a blazing-fast API, making it compatible with auto-updaters and modern mod managers.
      *   **Content Rich**: It's the home of the "Content Mod" revolution (Iris, Sodium, Lithium) which are essential for modern performance.

   .. tab-item:: 🟡 SpigotMC
      :sync: spigot

      **The Legacy Giant.**
      While it remains the largest repository, it suffers from years of technical debt and "abandonware."

      *   **The "Premium" Problem**: Spigot's premium resource section is often flooded with low-effort scripts and "lag fixers."
      *   **Manual Updates**: Most plugins on Spigot require manual downloads, which becomes a nightmare as your plugin list grows.
      *   **Vetting**: While there is moderation, it is less rigorous than Modrinth or Hangar.

   .. tab-item:: 🔴 Hangar & Others
      :sync: hangar

      *   **Hangar**: Built by the PaperMC team. It is highly vetted and focuses on "high-signal" plugins. If it's on Hangar, it's almost certainly high quality.
      *   **BuiltByBit**: Useful for professional services (graphics, setups), but be extremely cautious of "obfuscated" code that prevents you from seeing what the plugin is actually doing.

Evaluating Plugin Quality: The Deep Dive
----------------------------------------

Beyond a simple checklist, you need to understand *how* a plugin interacts with your server. A poorly written plugin can bring even the most powerful VPS to its knees.

The Essential Middleware: Library Plugins
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Many high-quality plugins require "Library" or "Bridge" plugins to function. These aren't bloat; they are standard APIs that allow different plugins to talk to each other.

*   **`Vault <https://www.spigotmc.org/resources/vault.34313/>`_**: The universal economy and permissions bridge. Almost every shop or chat plugin requires this.
*   **`PlaceholderAPI <https://api.extendedclip.com/placeholders/>`_**: Allows plugins to share information (e.g., showing a player's balance in a scoreboard).
*   **`ProtocolLib <https://www.spigotmc.org/resources/protocollib.1997/>`_**: Required by plugins that need to modify low-level Minecraft packets (e.g., custom tab lists or advanced anti-cheats).

.. dropdown:: 🚩 Red Flags: When to walk away

   *   **"Fixes Lag / Clears Entities"**: These are the biggest red flags in the industry. Minecraft's internal engine handles entity ticking; a plugin trying to "force" it usually causes more overhead than it saves.
   *   **Obfuscation**: If a developer hides their code (making it unreadable), you have to ask *why*. While common in premium plugins to prevent piracy, it is a massive security risk.
   *   **Dependency Hell**: If a small plugin requires five other "lib" plugins to function, it's often a sign of inefficient design.
   *   **"Pro" or "Plus" naming**: Often used to upsell basic features that should be in the base version.

Technical Performance: Sync vs. Async
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Minecraft's main logic runs on a single thread (the "Main Thread"). If a plugin tries to do something slow (like saving a large file or checking a database) on the main thread, the whole server freezes—this is what causes "TPS drops."

*   **Good Plugins**: Perform heavy lifting (Database, I/O, Web Requests) **Asynchronously** (on a separate thread).
*   **Bad Plugins**: Do everything on the main thread, causing "stutters" every time a player joins or a save occurs.

.. tip::

   Use the :doc:`optimization` tools (like Spark) to see which plugins are "hanging" your main thread. If a plugin shows up with a high percentage in ``/spark profiler open``, it's time to find an alternative.

   Additionally, having 50 modular plugins that do very few things often perform better than under 10
   large, bloated plugins that take up massive amounts of tick time. For reference, seek the Wikipedia article of
   the `Unix philosophy <https://en.wikipedia.org/wiki/Unix_philosophy>`_ of doing one thing, and do it well. 
   (Not: *Try to do everything and consistently fail at everything*)

The Danger of "Nulled" (Leaked) Plugins
---------------------------------------

It can be tempting to download a $20 premium plugin from a "leaks" site for free. **Don't do it.**

.. warning::

   **The Hidden Cost of "Free"**
   Leaked plugins are the #1 source of server backdoors. Malicious actors frequently take popular premium plugins, inject a "force-op" command or a credential stealer, and then upload them to leak sites.
   
   1.  **Backdoors**: They can give themselves OP or access your files.
   2.  **Performance**: Nulled plugins often have "anti-piracy" checks removed in ways that cause massive lag.
   3.  **No Support**: You can't update them, and you can't ask the developer for help when they inevitably break.

The Economy of Plugins: To Pay or Not to Pay?
---------------------------------------------

In the Minecraft world, "Premium" does not always mean "Better." In fact, many of the best tools
in the industry are free.

What is WORTH paying for?
~~~~~~~~~~~~~~~~~~~~~~~~~

You should only open your wallet for plugins that provide **groundbreaking functionality** or **extreme technical complexity** that cannot be replicated by FOSS alternatives.

.. list-table:: Justified Premium Purchases
   :widths: 30 70
   :header-rows: 1

   * - Category
     - Why it's worth it
      * - **Groundbreaking Effects**
        - Plugins like **`RealisticSeasons <https://www.spigotmc.org/resources/realisticseasons-1-16-3-1-21-11-seasons-in-your-minecraft-world-with-temperature-and-calendar.93275/>`_** or advanced shader-like world effects that fundamentally change the game's visuals and mechanics.
      * - **Custom Resource Managers**
        - Tools like **Oraxen** or **ItemsAdder**. These plugins allow you to add completely new 3D models, items, and UI elements to vanilla Minecraft without requiring players to install mods. The complexity of managing these resource packs and their logic is immense, making the price tag justified.
      * - **Advanced Anticheats**
        - While GrimAC (FOSS) is excellent, premium anticheats like **`Vulcan <https://www.spigotmc.org/resources/vulcan-anti-cheat-advanced-cheat-detection-1-8-1-21-11-folia-supported.83626/>`_** that provide dedicated support teams and frequent updates to counter new "ghost" cheats.
      * - **Complex Game Engines**
        - Custom RPG systems or highly complex minigame engines that saved you hundreds of hours of development time.
   
   What is NOT worth paying for?
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   
   Many developers prey on new administrators by charging for features that are natively available or available for free elsewhere.
   
   *   **"Optimization" Plugins**: **NEVER** pay for a plugin that claims to "fix lag" or "clear entities." These are almost always scams or placebo effects. Use native config tweaks instead.
   *   **Simple Chat Formatters**: There are dozens of free, high-quality chat formatters (like `LPC <https://modrinth.com/plugin/lpc-chat/versions>`_). Don't pay $20 for a colored prefix.
   *   **Basic GUIs**: Unless it comes with a massive pre-made configuration, you can build your own GUIs for free using modern tools like **Zmenus**.
   
   .. _testing_workflow:
   
   The Administrator's Testing Workflow
   ------------------------------------
   
   Never install a plugin directly onto your production server. Follow this workflow to ensure stability.
   
   .. mermaid::
   
      graph TD
         A[Find Plugin] --> B{FOSS?}
         B -- Yes --> C[Download from Modrinth/Hangar]
         B -- No --> D[Evaluate Price vs Value]
         D --> E[Purchase from Official Source]
         C --> F[Install on Local Test Server]
         E --> F
         F --> G[Check for Console Errors]
         G --> H[Run Spark Profiler]
         H --> I{Performance OK?}
         I -- No --> J[Uninstall/Find Alternative]
         I -- Yes --> K[Deploy to Production]
   
   1.  **The Sandbox**: Keep a copy of your server on a seperate server (or your PC). Test the plugin there first.
   2.  **Console Watch**: Look for "Stack Traces" or "Exceptions" during startup. Even if the plugin "works," these errors indicate poor code quality.
   3.  **The "Stress Test"**: If it's a gameplay plugin, invite a few friends to your test server and try to "break" the plugin. What happens if you spam a command? What happens if you disconnect while a menu is open?
   4.  **Final Review**: Only when you are 100% sure it won't crash your server should you move it to the production environment.

Running a cracked/offline mode server?
-------------------------

If you are running your server in ``offline-mode`` (not recommended for security reasons), you **must** use an
authentication plugin to prevent players from impersonating one another or staff member.

.. grid:: 1 1 2 2
   :gutter: 2

   .. grid-item-card:: ✅ Recommended: AuthMeReloaded
      :link: https://modrinth.com/plugin/authmerereloaded

      `AuthMeReloaded <https://modrinth.com/plugin/authmerereloaded>`_ is an actively maintained fork of the original AuthMe. It is exceptionally stable, feature-rich, and better than 95% of other authentication plugins on the market.

   .. grid-item-card:: ❌ Avoid: OpeNLogin
      :class-header: sd-bg-danger sd-text-white

      Be extremely cautious of **OpeNLogin** by NickUC. While it appears to be yet another alternative,
      it is essentially adware for his premium ``nLogin`` plugin. Even though there is a toggle in the
      ``config.yml`` to disable "advertising," it is known to continue pushing adverts regardless of the setting.

.. seealso::

      * :doc:`optimization`: Learn how to use Spark to verify plugin performance.
      * :doc:`plugin_alternatives`: Our curated list of FOSS replacements for expensive plugins.
