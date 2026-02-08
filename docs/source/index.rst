Welcome to OpenWiki
===================================

**OpenWiki** is an uncensored wiki for server ownership (especially administration) for *Minecraft: Java Edition*.

.. tip::

   This wiki is built for **low-budget server creation and moderation**. We are here to prove that "premium" doesn't always mean good. Most of the tools and software recommended here are Free and Open Source (FOSS).

The Administrator's Roadmap
---------------------------

Setting up a professional-grade server can be daunting. Follow this step-by-step guide to go from a blank folder to a thriving community.

.. grid:: 1 1 2 2
   :gutter: 3

   .. grid-item-card:: 1. Choosing a Host
      :link: hosting
      :link-type: doc

      Don't fall for "unlimited" traps. Learn why VPS hosting is superior to managed hosting and how to find real hardware.
      ^^^
      **Key Task**: Compare providers and avoid "Summer Hosts" with impossible pricing.

   .. grid-item-card:: 2. Preparation & Environment
      :link: first_server
      :link-type: doc

      Once you have your host, you need a solid environment. Install the correct Java version and prepare your OS (Windows, Linux, or macOS).
      ^^^
      **Key Task**: Install Java 21 and configure your user permissions.

   .. grid-item-card:: 3. Software Selection
      :link: first_server
      :link-type: doc

      Choose the right "flavor" of Minecraft. For most, PaperMC is the standard, while PurpurMC offers more "fun" tweaks.
      ^^^
      **Key Task**: Download the latest build of Paper or Purpur.

   .. grid-item-card:: 4. Plugin Selection & Evaluation
      :link: plugin_guide
      :link-type: doc

      Don't bloat your server. Learn where to find high-quality plugins and how to avoid "premium" scams.
      ^^^
      **Key Task**: Choose your core plugins and verify their source.

   .. grid-item-card:: 5. Core Configuration
      :link: first_server
      :link-type: doc

      Understand ``server.properties`` and the hidden performance toggles that stop lag before it starts.
      ^^^
      **Key Task**: Set simulation distance to 5 and enable online-mode.

   .. grid-item-card:: 6. Launching & JVM Tuning
      :link: first_server
      :link-type: doc

      Don't just double-click a JAR. Use Aikar's Flags or ZGC to ensure smooth gameplay without "Lag Spikes."
      ^^^
      **Key Task**: Create a startup script with optimized memory flags.

   .. grid-item-card:: 7. Optimization
      :link: optimization
      :link-type: doc

      Squeeze every drop of performance. Pre-generate your world and tune entity activation ranges to save CPU cycles.
      ^^^
      **Key Task**: Use the Chunky plugin to pre-generate a 5,000-block radius.

   .. grid-item-card:: 8. Security & Stability
      :link: security
      :link-type: doc

      Protect your hard work. Set up LuckPerms, land claims, and automated off-site backups.
      ^^^
      **Key Task**: Install LuckPerms and configure a daily backup schedule.

   .. grid-item-card:: 9. Networking & Access
      :link: networking
      :link-type: doc

      Open your doors to the world. Learn about port forwarding, VPS hosting, and DDoS protection.
      ^^^
      **Key Task**: Configure your firewall and point a domain to your IP.

   .. grid-item-card:: 10. Maintenance & Debugging
      :link: troubleshooting
      :link-type: doc

      A server is a living thing. Learn how to update safely and monitor performance with Spark.
      ^^^
      **Key Task**: Run a Spark profiler to identify performance bottlenecks.

Avoid Common Pitfalls
---------------------

Don't let your project fail before it even starts. Learn from the mistakes of others.

*   **The Plugin Guide**: Learn how to evaluate plugins and avoid overpaying for features.
    | :doc:`plugin_guide`
*   **Networking & Proxies**: Learn how to scale your server and support Bedrock players.
    | :doc:`networking`
*   **Troubleshooting**: Master the art of reading logs and fixing crashes.
    | :doc:`troubleshooting`
*   **The FOSS Alternative Table**: Don't overspend. Many "premium" plugins have high-quality free and open-source alternatives.
    | :doc:`plugin_alternatives`
*   **Summer Hosts**: Learn how to spot fly-by-night hosting companies that will disappear with your money.
    | :doc:`summer_hosts`
*   **The Hall of Shame**: A historical record of hosting failures and scams to avoid.
    | :doc:`hall_of_shame`
*   **Jargon Buster**: Confused by terms like "TPS," "Heap," or "Fork"?
    | :doc:`glossary`

.. note::

   If you wish to download this project as an archived PDF/EPUB file,
   click the ⑂ icon on the bottom right corner that reads "⑂ latest ▾".
   Click the downwards pointing arrow (▾), and you can now select the preferred download method,
   PDF or EPUB. Choose your preferred method.

Contents
--------

.. toctree::
   :maxdepth: 2
   :hidden:

   hosting
   first_server
   plugin_guide
   optimization
   networking
   troubleshooting
   plugin_alternatives
   security
   summer_hosts
   hall_of_shame
   glossary
