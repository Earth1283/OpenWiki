Welcome to OpenWiki
===================================

**OpenWiki** is an uncensored, community-driven guide for Minecraft server administrators. We focus on technical excellence, financial transparency, and the power of Open Source.

.. note::

   **Unbiased Recommendations**: All software, services, and hosting providers recommended here are selected solely for performance and utility. We are **not** sponsored by any entity.

Our Philosophy
--------------

*   **FOSS First**: If a free, open-source tool exists that matches or exceeds a "premium" one, we will always recommend the FOSS option.
*   **Technical Truth**: We don't use marketing buzzwords. If a host says "Unlimited," we'll explain why they're lying.
*   **Performance Focused**: We prioritize Ticks Per Second (TPS) and player experience above all else.

The Administrator's Roadmap
---------------------------

Phase 1: Foundation & Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. grid:: 1 1 2 2
   :gutter: 3

   .. grid-item-card:: 1. Choosing a Host
      :link: hosting
      :link-type: doc

      Don't fall for "unlimited" traps. Learn why VPS hosting is superior to managed hosting. For power users, see our :doc:`vps_hosting` guide.
      ^^^
      **Key Task**: Compare providers and avoid "Summer Hosts."

   .. grid-item-card:: 2. OS & Java Setup
      :link: first_server
      :link-type: doc

      Configure your environment correctly. Install Java 21 and set up user permissions.
      ^^^
      **Key Task**: Set up a non-root user and install the JRE.

   .. grid-item-card:: 3. Software Selection
      :link: first_server
      :link-type: doc

      Choose between Paper, Purpur, or Folia based on your server's goals.
      ^^^
      **Key Task**: Download and verify your server JAR.

Phase 2: Configuration & Performance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. grid:: 1 1 2 2
   :gutter: 3

   .. grid-item-card:: 4. Plugin Evaluation
      :link: plugin_guide
      :link-type: doc

      Learn where to find high-quality plugins and how to avoid "premium" scams.
      ^^^
      **Key Task**: Audit your plugin list for "Main Thread" bloat.

   .. grid-item-card:: 5. Core Optimization
      :link: optimization
      :link-type: doc

      Squeeze every drop of performance from your CPU.
      ^^^
      **Key Task**: Pre-generate worlds and tune entity activation.

   .. grid-item-card:: 6. Security & Backups
      :link: security
      :link-type: doc

      Protect your data and your players.
      ^^^
      **Key Task**: Configure LuckPerms and off-site backups.

Phase 3: Scaling & Community
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. grid:: 1 1 2 2
   :gutter: 3

   .. grid-item-card:: 7. Networking & Proxies
      :link: networking
      :link-type: doc

      Link multiple servers and protect your backend IP.
      ^^^
      **Key Task**: Set up Velocity and Geyser for Bedrock support.

   .. grid-item-card:: 8. Debugging & Maintenance
      :link: troubleshooting
      :link-type: doc

      A server is a living thing. Learn how to monitor and fix issues.
      ^^^
      **Key Task**: Use Spark to identify performance bottlenecks.

Avoid Common Pitfalls
---------------------

.. grid:: 1 2 2 2
   :gutter: 2

   .. grid-item-card:: 🛑 The "Summer Host" Trap
      :link: summer_hosts
      :link-type: doc
      :class-header: sd-bg-danger sd-text-white

      Learn to spot fly-by-night companies before they take your money.

   .. grid-item-card:: 💸 Premium Scams
      :link: plugin_alternatives
      :link-type: doc
      :class-header: sd-bg-warning sd-text-white

      Stop overpaying. Find high-quality FOSS alternatives to "Pro" plugins.

   .. grid-item-card:: 📜 Jargon Buster
      :link: glossary
      :link-type: doc
      :class-header: sd-bg-info sd-text-white

      Confused by terms like "TPS," "Heap," or "Folia"? We break it down.

   .. grid-item-card:: 💀 The Hall of Shame
      :link: hall_of_shame
      :link-type: doc
      :class-header: sd-bg-dark sd-text-white

      A historical record of hosting failures and community scams.

.. note::

   If you wish to download this project as an archived PDF/EPUB file, click the ⑂ icon on the bottom right corner.

Contents
--------

.. toctree::
   :maxdepth: 4

   hosting
   vps_hosting
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
