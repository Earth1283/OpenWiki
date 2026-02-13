Server Security
===============

Running a public Minecraft server exposes you to various risks, from simple "griefing" to malicious attacks on your network. This guide covers the essentials of keeping your server and its players safe.

Permissions Management
----------------------
Never give a player "OP" unless you trust them with your life. Instead, use a permissions plugin.

*   `LuckPerms <https://luckperms.net/>`_: The absolute industry standard and one of the most feature-rich permissions plugins available. It allows you to create groups (e.g., Member, Moderator, Admin) and give them specific nodes (e.g., `minecraft.command.gamemode`) through an intuitive web editor.

.. dropdown:: 🛠️ The LuckPerms Workflow
   :open:

   1.  **Generate a Link**: Run ``/lp editor`` in-game or from the console.
   2.  **Edit Permissions**: Click the link to open the web editor. Create groups, add permissions nodes, and set prefixes/suffixes.
   3.  **Apply Changes**: Once done, click "Save" in the top right. Copy the command provided (e.g., ``/lp applyedits <key>``) and paste it back into your server console.
   4.  **Verify**: Check a player's permissions with ``/lp user <name> info``.

Avoid using old plugins like Essentials GroupManager or PermissionsEx, as they are no longer maintained and can have security flaws.

Grief Prevention
----------------
:term:`Griefing` is the act of destroying or defacing another player's work.

.. tab-set::

   .. tab-item:: Rollback Plugins

      *   `Prism <https://github.com/Prism-MC/Prism>`_: **Highly Recommended** for servers on version **1.21.4 or higher**. Unlike older tools, Prism allows you to *preview* rollbacks before applying them and can successfully roll back entities (like item frames and armor stands).
      *   `CoreProtect <https://coreprotect.net/>`_: The classic choice for older versions. It logs every block break, placement, and chest transaction.

   .. tab-item:: Land Claiming

      *   `Dominion <https://github.com/Zrips/Dominion>`_: A modern and powerful alternative to traditional claiming systems. It offers a robust set of flags and a user-friendly interface for managing player "properties."
      *   `GriefPrevention <https://github.com/TechFortress/GriefPrevention>`_: The classic "golden shovel" land claiming plugin.

   .. tab-item:: World Protection

      *   `WorldGuard <https://enginehub.org/worldguard/>`_: Allows you to create "Regions" where building or PvP is disabled (e.g., your server spawn).

.. note::

   Most grief prevention plugins require a permissions plugin like `LuckPerms <https://luckperms.net/>`_ to function correctly.

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

Protecting your server requires a multi-layered approach to ensure that even if one layer is bypassed, the others remain intact.

.. mermaid::

   graph TD
       Player((Player)) --> Edge[Edge: Cloudflare / TCPShield]
       Edge --> FW[Host: UFW Firewall]
       FW --> Proxy[Proxy: Velocity]
       Proxy --> Backend[Backend: Paper/Purpur]
       
       subgraph Protected Network
           direction TB
           FW
           Proxy
           Backend
       end
       
       style Edge fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#01579b
       style FW fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,color:#1b5e20
       style Proxy fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,color:#1b5e20
       style Backend fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,color:#1b5e20

Firewalls
~~~~~~~~~

If you are hosting from home or a VPS, ensure your firewall (e.g., `ufw` on Linux) only allows traffic on necessary ports (usually `25565`).



.. caution::



   Opening ports on your home router can be dangerous if not done correctly. Always use a firewall on the host machine as well.



VPS Hardening
~~~~~~~~~~~~~

If you are using a VPS, the default configuration is often insecure. Take these steps immediately:

1.  **Disable Root Login**: Edit ``/etc/ssh/sshd_config`` and set ``PermitRootLogin no``.
2.  **SSH Keys**: Disable password-based login by setting ``PasswordAuthentication no`` in the same file.
3.  **Change the SSH Port**: Moving SSH from port 22 to something else (e.g., 2222) will stop 99% of automated "bot" scans.
4.  **Fail2Ban**: Install it to automatically ban malicious IPs.

.. code-block:: bash

   # 1. Update and install Fail2Ban
   sudo apt update && sudo apt install fail2ban -y

   # 2. Configure Firewall (UFW)
   sudo ufw allow 2222/tcp  # Your new SSH port
   sudo ufw allow 25565/tcp # Minecraft
   sudo ufw enable

   # 3. Restart SSH to apply changes
   sudo systemctl restart ssh



Plugin Safety & Backdoors

-------------------------



Not every plugin developer has good intentions. A "Backdoor" is a hidden piece of code that allows the developer (or an attacker) to gain control of your server.



How to Spot a Suspicious Plugin:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



*   **Requesting Weird Permissions**: A "Chat" plugin should never ask for permission to access your filesystem or run shell commands.

*   **Obfuscated Code**: If you open a plugin JAR and the code looks like gibberish (`a.b.c()`), be extremely cautious. This is often used to hide malicious logic.

*   **"Force-OP" Commands**: Some malicious plugins include hidden commands (e.g., `/help <secret_key>`) that give the user full Administrator rights.

*   **Automatic Updates from Unknown Sources**: Only use plugins that update from trusted platforms like Modrinth or Hangar.



.. tip::



   Use the **"Administrator's Testing Workflow"** found in the :doc:`plugin_guide` to verify every plugin in a sandbox before moving it to your main server.



Anti-Bot Protection

~~~~~~~~~~~~~~~~~~~



Bot attacks can flood your server with hundreds of fake players, crashing the :term:`JVM`.



*   `Sonar <https://github.com/flyte-dev/sonar>`_: A highly effective, free, and "out-of-the-box" anti-bot solution. It is extremely performant and requires almost zero configuration to start blocking bot attacks.



DDOS Protection

~~~~~~~~~~~~~~~

Let's be realistic: 99.9% of Minecraft servers are **never** subject to a high-level, sophisticated DDoS attack. Most "attacks" you will encounter are simply kids using low-effort "booters" that can be easily mitigated.



*   `TCPShield <https://tcpshield.com/>`_: For the vast majority of server owners, **TCPShield's free tier** is more than enough to protect your backend IP and handle basic attacks.

*   **Hosting Providers**: Most reputable Minecraft hosts (e.g., `Bloom.host <https://bloom.host/>`_, `Pufferfish Host <https://pufferfish.host/>`_) provide sufficient built-in protection at the network level.



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



*   **The FOSS Solution**: Use `GrimAC <https://github.com/GrimAnticheat/Grim>`_ or `Lightning GrimAC <https://github.com/Lightning-AntiCheat/Lightning>`_. These are extremely effective, open-source, and provide high-quality movement checks for free.

*   **The Premium Option**: If you have the budget, `Vulcan <https://www.spigotmc.org/resources/vulcan-advanced-cheat-detection-1-7-1-21.83626/>`_ is a highly regarded paid anti-cheat, but for most servers, the FOSS options above are more than sufficient.
