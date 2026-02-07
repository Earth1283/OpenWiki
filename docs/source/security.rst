Server Security
===============

Running a public Minecraft server exposes you to various risks, from simple "griefing" to malicious attacks on your network. This guide covers the essentials of keeping your server and its players safe.

Permissions Management
----------------------
Never give a player "OP" unless you trust them with your life. Instead, use a permissions plugin.

*   **LuckPerms**: The absolute industry standard and one of the most feature-rich permissions plugins available. It allows you to create groups (e.g., Member, Moderator, Admin) and give them specific nodes (e.g., `minecraft.command.gamemode`) through an intuitive web editor.

Avoid using old plugins like Essentials GroupManager or PermissionsEx, as they are no longer maintained and can have security flaws.

Grief Prevention
----------------
:term:`Griefing` is the act of destroying or defacing another player's work.

.. tab-set::

   .. tab-item:: Rollback Plugins

      *   **Prism**: **Highly Recommended** for servers on version **1.21.4 or higher**. Unlike older tools, Prism allows you to *preview* rollbacks before applying them and can successfully roll back entities (like item frames and armor stands).
      *   **CoreProtect**: The classic choice for older versions. It logs every block break, placement, and chest transaction.

   .. tab-item:: Land Claiming

      *   **Dominion**: A modern and powerful alternative to traditional claiming systems. It offers a robust set of flags and a user-friendly interface for managing player "properties."
      *   **GriefPrevention**: The classic "golden shovel" land claiming plugin.

   .. tab-item:: World Protection

      *   **WorldGuard**: Allows you to create "Regions" where building or PvP is disabled (e.g., your server spawn).

.. note::

   Most grief prevention plugins require a permissions plugin like **LuckPerms** to function correctly.

Backups: Your Last Line of Defense
----------------------------------
Hardware fails, plugins bug out, and humans make mistakes. Without a backup, a single error can lose months of work.

.. sidebar:: Backup Frequency

   * **Busy Servers**: Every 4-6 hours.
   * **Small Servers**: Every 24 hours.

.. tabs::

   .. tab:: Local Backups

      Fastest to restore but vulnerable to disk failure. Keep these on a separate internal physical drive if possible.

   .. tab:: Off-site Backups

      Essential for disaster recovery. Use services like S3, Google Drive, or Backblaze B2.

   .. tab:: Database Backups

      If you use MySQL/PostgreSQL for plugins like CoreProtect or LuckPerms, don't forget to export your databases!

*   **Off-site Storage**: Never keep your backups only on the same disk as your server. Use S3, Google Drive, or a separate physical drive.

Network Security
----------------

Firewalls
~~~~~~~~~
If you are hosting from home or a VPS, ensure your firewall (e.g., `ufw` on Linux) only allows traffic on necessary ports (usually `25565`).

.. caution::

   Opening ports on your home router can be dangerous if not done correctly. Always use a firewall on the host machine as well.

Anti-Bot Protection
~~~~~~~~~~~~~~~~~~~
Bot attacks can flood your server with hundreds of fake players, crashing the :term:`JVM`.

*   **Sonar**: A highly effective, free, and "out-of-the-box" anti-bot solution. It is extremely performant and requires almost zero configuration to start blocking bot attacks.

DDOS Protection
~~~~~~~~~~~~~~~
Let's be realistic: 99.9% of Minecraft servers are **never** subject to a high-level, sophisticated DDoS attack. Most "attacks" you will encounter are simply kids using low-effort "booters" that can be easily mitigated.

*   **TCPShield**: For the vast majority of server owners, **TCPShield's free tier** is more than enough to protect your backend IP and handle basic attacks.
*   **Hosting Providers**: Most reputable Minecraft hosts (e.g., Bloom.host, Pufferfish Host) provide sufficient built-in protection at the network level.

Avoid overpaying for "enterprise-grade" protection if you are just running a community server; the free tools available today are incredibly capable.

Whitelisting
------------
If you only want to play with a specific group of friends, enable the whitelist:

.. code-block:: bash

    /whitelist on
    /whitelist add username

Anti-Cheat
----------
Even if your server is small, "hackers" using clients like Meteor or Aristois will eventually find it.

.. important::

   Vanilla Minecraft has very weak movement checks. Modern :term:`fork` software like Paper improves this, but dedicated plugins are still recommended.

*   **The FOSS Solution**: Use **GrimAC** or **Lightning GrimAC**. These are extremely effective, open-source, and provide high-quality movement checks for free.
*   **The Premium Option**: If you have the budget, **Vulcan** is a highly regarded paid anti-cheat, but for most servers, the FOSS options above are more than sufficient.