Identifying "Summer Hosts"
==========================

In the Minecraft community, a **"Summer Host"** is a term used to describe a short-lived hosting company, often started by a teenager during their summer break. While they usually offer extremely low prices, they almost always fail within months, leading to total data loss for their customers.

.. admonition:: The Golden Rule
   :class: danger

   If the price seems too good to be true, it is. You aren't paying for the RAM; you're paying for the stability, support, and network quality.

The Summer Host Bingo
---------------------

How many of these boxes does your potential host check? Use this grid to evaluate their legitimacy. **Click a tile to mark it.**

.. raw:: html

   <div id="bingo-score" style="font-size: 1.5em; font-weight: bold; margin-bottom: 20px; text-align: center; padding: 10px; background: #f8f9fa; border-radius: 8px; border: 2px solid #dee2e6;">
      Bingo Score: <span id="score-val">0</span> / 9
   </div>

   <style>
      .bingo-tile {
         cursor: pointer;
         transition: all 0.3s ease !important;
      }
      .bingo-tile:hover {
         transform: translateY(-5px);
         box-shadow: 0 4px 15px rgba(0,0,0,0.1) !important;
      }
      .bingo-tile.marked {
         background-color: #ffcccc !important;
         border-color: #ff0000 !important;
         opacity: 0.8;
      }
      .bingo-tile.marked .sd-card-header {
         background-color: #ff0000 !important;
         color: white !important;
      }
      .bingo-tile.marked::after {
         content: "❌";
         position: absolute;
         top: 50%;
         left: 50%;
         transform: translate(-50%, -50%);
         font-size: 5em;
         opacity: 0.2;
         pointer-events: none;
      }
   </style>

   <script>
      document.addEventListener('DOMContentLoaded', function() {
         const cards = document.querySelectorAll('.bingo-tile');
         const scoreVal = document.getElementById('score-val');
         let score = 0;
         const winSound = new Audio('https://www.myinstants.com/media/sounds/among-us-role-reveal-sound.mp3');

         cards.forEach(card => {
            card.addEventListener('click', function() {
               this.classList.toggle('marked');
               score = document.querySelectorAll('.bingo-tile.marked').length;
               scoreVal.innerText = score;
               
               if (score >= 5) {
                  document.getElementById('bingo-score').style.borderColor = 'red';
                  document.getElementById('bingo-score').style.color = 'red';
               } else {
                  document.getElementById('bingo-score').style.borderColor = '#dee2e6';
                  document.getElementById('bingo-score').style.color = 'inherit';
               }

               if (score === 9 && this.classList.contains('marked')) {
                  winSound.play();
               }
            });
         });
      });
   </script>

.. grid:: 1 2 3 3
   :gutter: 3

   .. grid-item-card:: 💰 Unrealistic Pricing
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Offering "Unlimited" RAM or $1/GB for high-end Ryzen CPUs.

   .. grid-item-card:: 🎨 Free Web Template
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      The website uses a stock "host" template without any custom branding.

   .. grid-item-card:: 🗨️ Discord Only
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Support is exclusively through Discord; no professional ticket system.

   .. grid-item-card:: 🔒 No Legal Info
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      No registered business address, TOS, or Privacy Policy in the footer.

   .. grid-item-card:: 📈 Oversold Nodes
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Claims 100% CPU usage is "normal" because they put 100 servers on one CPU.

   .. grid-item-card:: 📅 "New" Company
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      The domain was registered less than 3 months ago.

   .. grid-item-card:: 🚩 "Custom" Bot
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Their Discord bot is just a renamed public bot (like MEE6 or Dyno).

   .. grid-item-card:: 💸 No Tax Info
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Prices don't include VAT or equivalent where required by law.

   .. grid-item-card:: 📢 Mass Pings
      :class-header: sd-bg-warning
      :class-card: bingo-tile

      Frequent @everyone in Discord for minor updates or "owner" mood swings.

Common Red Flags
----------------

.. tab-set::

   .. tab-item:: Technical Signs

      * **`Pterodactyl <https://pterodactyl.io/>`_ Default**: Zero customization to the panel.
      * **No Backups**: They expect you to handle all backups manually.
      * **DDoS Claims**: Claiming "unmetered" protection from a provider like Hetzner (which actually has weak game-layer filtering).

   .. tab-item:: Business Signs

      * **PayPal Personal**: Asking you to pay via "Friends and Family."
      * **Owner Age**: The "CEO" is 15 years old and doesn't have a legal entity.
      * **Summer Launch**: They magically appear in June and disappear by September.

How to Verify a Host
--------------------

1. **Check the Domain Age**: Use a `WHOIS lookup tool <https://who.is/>`_. If it's brand new, be wary.
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

The "Unlimited" Myth
--------------------

.. admonition:: Physics 101
   :class: error

   **Unlimited resources do not exist.** Any host promising "Unlimited RAM," "Unlimited CPU," or "Unlimited NVMe Storage" is lying to you.

Computing resources are finite. A physical server has a set amount of RAM sticks and CPU cycles. When a host offers "Unlimited" plans, they are counting on you not actually using the resources. The moment your server starts to grow, they will suspend you for "excessive usage"—the very thing they promised was unlimited.

*   **RAM**: Cannot be "unlimited." The :term:`JVM` requires a specific amount of memory to be allocated via the :term:`Heap`.
*   **CPU**: You are sharing a physical processor with dozens of other people. You cannot have "unlimited" shares of a finite pie.
*   **Disk**: Hard drives have physical capacities. "Unlimited" disk space usually means they will ban you if you store more than 10-20GB of backups or world files.

.. tip::

   If you find a host using a ToS that still has placeholders like ``[Company Name]`` or ``[Governing Law]``, **close the tab immediately**. It is a 100% guarantee that the host is a fly-by-night operation.
