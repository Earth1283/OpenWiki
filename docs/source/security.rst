Server Security
===============

Running a public Minecraft server exposes you to various risks, from simple "griefing" to malicious attacks on your network. This guide covers the essentials of keeping your server and its players safe.

Permissions Management
----------------------
Never give a player "OP" unless you trust them with your life. Instead, use a permissions plugin.

*   **LuckPerms**: The gold standard for permissions. It allows you to create groups (e.g., Member, Moderator, Admin) and give them specific nodes (e.g., `minecraft.command.gamemode`).

Avoid using old plugins like Essentials GroupManager or PermissionsEx, as they are no longer maintained and can have security flaws.

Grief Prevention
----------------
:term:`Griefing` is the act of destroying or defacing another player's work.

*   **CoreProtect**: This is a mandatory plugin for any survival server. It logs every block break, placement, and chest transaction.
*   **WorldGuard**: Allows you to create "Regions" where building or PvP is disabled (e.g., your server spawn).
*   **GriefPrevention**: A popular plugin that lets players "claim" land with a golden shovel.

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

DDOS Protection
~~~~~~~~~~~~~~~
Minecraft servers are frequent targets for Distributed Denial of Service (DDoS) attacks.

*   **Hosting Providers**: Most reputable Minecraft hosts (e.g., Bloom.host, Pufferfish Host, etc.) provide built-in DDoS protection.
*   **Proxies**: Services like `TCPShield` or `Cloudflare Spectrum` can hide your actual server IP behind a protected proxy.

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

*   **The Solution**: Use a modern anti-cheat plugin like `GrimAC` (free and very effective for movement) or `Vulcan` (paid, very comprehensive).

