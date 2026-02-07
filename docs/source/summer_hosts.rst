Identifying "Summer Hosts"
==========================

In the Minecraft community, a **"Summer Host"** is a term used to describe a short-lived hosting company, often started by a teenager during their summer break. While they usually offer extremely low prices, they almost always fail within months, leading to total data loss for their customers.

.. admonition:: The Golden Rule
   :class: danger

   If the price seems too good to be true, it is. You aren't paying for the RAM; you're paying for the stability, support, and network quality.

The Summer Host Bingo
---------------------

How many of these boxes does your potential host check? Use this grid to evaluate their legitimacy.

.. grid:: 1 2 3 3
   :gutter: 3

   .. grid-item-card:: 💰 Unrealistic Pricing
      :class-header: sd-bg-warning

      Offering "Unlimited" RAM or $1/GB for high-end Ryzen CPUs.

   .. grid-item-card:: 🎨 Free Web Template
      :class-header: sd-bg-warning

      The website uses a stock "host" template without any custom branding.

   .. grid-item-card:: 🗨️ Discord Only
      :class-header: sd-bg-warning

      Support is exclusively through Discord; no professional ticket system.

   .. grid-item-card:: 🔒 No Legal Info
      :class-header: sd-bg-warning

      No registered business address, TOS, or Privacy Policy in the footer.

   .. grid-item-card:: 📈 Oversold Nodes
      :class-header: sd-bg-warning

      Claims 100% CPU usage is "normal" because they put 100 servers on one CPU.

   .. grid-item-card:: 📅 "New" Company
      :class-header: sd-bg-warning

      The domain was registered less than 3 months ago.

Common Red Flags
----------------

.. tab-set::

   .. tab-item:: Technical Signs

      * **Pterodactyl Default**: Zero customization to the panel.
      * **No Backups**: They expect you to handle all backups manually.
      * **DDoS Claims**: Claiming "unmetered" protection from a provider like Hetzner (which actually has weak game-layer filtering).

   .. tab-item:: Business Signs

      * **PayPal Personal**: Asking you to pay via "Friends and Family."
      * **Owner Age**: The "CEO" is 15 years old and doesn't have a legal entity.
      * **Summer Launch**: They magically appear in June and disappear by September.

How to Verify a Host
--------------------

1. **Check the Domain Age**: Use a WHOIS lookup tool. If it's brand new, be wary.
2. **Audit the Hardware**: Don't take their word for it. Use a specialized tool to see what is actually under the hood.

   .. card:: 🛠️ HardwareAudit Plugin
      :class-header: sd-bg-dark sd-text-white

      The most reliable way to verify hardware is to run an audit from *inside* the server.
      ^^^
      Download the latest `.jar` from the `HardwareAudit Release Folder <https://github.com/Earth1283/HardwareAudit>`_.
      
      * **Note**: A new obfuscated build with a unique SHA-256 hash is generated every 24 hours to prevent tampering.
      * **Command**: Run ``/audit all`` to reveal the **REAL** CPU model, core counts, and storage speeds. 
      
      If the results don't match what you paid for (e.g., you see an Intel Xeon when they promised a Ryzen 7950X), you are being scammed.

3. **Analyze the Paperwork**: Summer hosts often have "legal" documents full of holes.

Deceptive ToS and Refund Policies
---------------------------------

Before you pay, read their Terms of Service (ToS) and Refund Policy. Summer hosts often use unedited templates that contain the following red flags:

.. list-table:: ToS Red Flags
   :widths: 30 70
   :header-rows: 1

   * - The Red Flag
     - Why it's Dangerous
   * - ``[Insert State/Country Here]``
     - They didn't even read their own ToS. This document is legally non-binding and shows total lack of professionalism.
   * - "We reserve the right to cancel for any reason"
     - This is often used as a "get out of jail free" card to terminate your server and keep your money if you complain about lag.
   * - "No refunds under any circumstances"
     - Legitimate businesses offer pro-rated refunds or at least a 24-72 hour money-back guarantee.
   * - Lack of a Privacy Policy
     - They may be selling your email or Discord data to other low-quality hosts.

.. tip::

   If you find a host using a ToS that still has placeholders like ``[Company Name]`` or ``[Governing Law]``, **close the tab immediately**. It is a 100% guarantee that the host is a fly-by-night operation.
