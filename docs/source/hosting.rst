Choosing a Hosting Provider
===========================

Selecting where to host your server is the most critical decision you will make. A poor choice leads to lag, downtime, and potential data loss. This guide will help you navigate the complex landscape of Minecraft hosting.

VPS vs. Managed Hosting
-----------------------

There are two primary ways to host a Minecraft server: **Virtual Private Servers (VPS)** and **Managed Minecraft Hosting** (often called "shared hosting").

.. mermaid::

   graph TD
       Start[Ready to Host?] --> Q1{Do you know Linux?}
       Q1 -- No --> Q2{Want to learn?}
       Q1 -- Yes --> VPS[VPS Hosting]
       Q2 -- Yes --> VPS
       Q2 -- No --> Managed[Managed Hosting]
       
       style VPS fill:#e1f5fe,stroke:#01579b,color:#01579b
       style Managed fill:#fce4ec,stroke:#880e4f,color:#880e4f

.. tab-set::

   .. tab-item:: 🐧 VPS (Highly Recommended)

      A VPS gives you a slice of a physical server with your own Operating System (usually Linux).

      *   **Control**: You have full root access. You can install any Java version, any database, and any monitoring tools you want.
      *   **Learning**: You will learn valuable Linux administration skills.
      *   **Verdict**: **Best for serious administrators** who want stability and growth.

      .. seealso::
         
         For a deep dive into setting up and optimizing a VPS, see our dedicated guide: :doc:`vps_hosting`.

   .. tab-item:: 🧊 Managed Hosting

      These providers use a control panel (like Pterodactyl) to let you upload a JAR and click "Start".
      It shields you from the complexity of the real host on a VPS. As a trade-off, you will have a much
      simpler and "dumber" config system.

      *   **Ease of Use**: No Linux knowledge required.
      *   **Overselling**: Many providers "oversell" their nodes, putting too many servers on one CPU, leading to "stuttering."
      *   **The "Unlimited" Lie**: Many claim "unlimited" resources which don't actually exist (see below).
      *   **Verdict**: Only suitable for small, private servers with a few friends.

What to Look for in Hardware
----------------------------

Minecraft is **mostly single-threaded** (except Folia). This means that a CPU with 64 slow cores is significantly worse than a CPU with 4 very fast cores.

1.  **CPU Model**: Look for high-frequency modern CPUs.
    *   **Excellent**: Ryzen 9 7950X, Ryzen 9 5950X, Intel i9-14900K.
    *   **Good**: Ryzen 7 5800X, Intel i7-12700K, or Zen3 or Zen4 AMD EPYCs are acceptable too
    *   **Avoid**: Intel Xeon E5 series (too old/slow), "Intel Core" with no model number.
2.  **Storage**: Only accept **NVMe SSDs**. Standard SATA SSDs or HDDs will cause major lag during world saving and chunk loading, though modern SATA SSDs have mostly neutralized the issue.
3.  **RAM**: 8GB to 32GB is the sweet spot for most community servers. Anything more than 32GB for a single instance often requires advanced :term:`Garbage Collector (GC)` tuning.

The Anatomy of a Great Host
---------------------------

A "good" host is more than just a fast CPU. Look for these pillars of quality when making your final decision:

*   **Hardware Transparency**: They don't just say "i9" or "Ryzen." They specify the exact model (e.g., Ryzen 9 7950X) and allow you to verify it.
*   **Network Quality**: They use high-quality upstream providers (like `Corero <https://www.corero.com/>`_, `Path <https://path.net/>`_, or `Cosmic Guard <https://www.cosmicguard.com/>`_ for DDoS protection) and offer "Looking Glass" tools (a test IP or web portal) so you can test your ping and latency before buying.
*   **Technical Support**: The staff should actually understand Minecraft. If you ask about "Aikar's Flags" or "Spark Profiling" and they don't know what you mean, they aren't equipped to help you.
*   **Off-site Backups**: A great host offers (or includes) backups that are stored in a completely different data center. If their building burns down, your data should still be safe.
*   **A Solid Track Record**: Look for providers that have been in business for at least 2+ years. Most "Summer Hosts" fail within their first 6 months.

The "Summer Host" Trap
----------------------

A :doc:`summer_hosts` is a fly-by-night operation started by someone with no business experience.
The person (usually referred to as the CEO by themselves) typically belongs to the demographic
of young adults, which is fitting, considering that the people who fall victim to the scam often
belong to such demographics.

They often disappear when school starts, taking your money and your world files with them.

.. warning::

   **🚩 RED FLAGS 🚩**

   **Impossibly Low Pricing** is the #1 red flag. If you see a host offering a Ryzen 7950X for $1/GB of RAM, they are either lying about the hardware or overselling the node so heavily that your server will be unplayable.

   **Unlimited Resources** is physically impossible. There is a finite quantity of particles in the universe, so is compute.

Physically Impossible Pricing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Consider the math: A high-end dedicated server costs roughly $100-$200 per month and has 128GB of RAM.
*   If a host sells RAM at $1/GB, they only make $128 if the node is 100% full.
*   After payment processing fees, taxes, and staff costs, they are **losing money**.
*   **The Result**: They will eventually exit-scam (shut down without notice) or drastically reduce performance to survive.

So what will they do to keep themselves alive? They will begin to oversell their nodes!

Knowing the single-threaded design of Minecraft servers, they will try to fit around :math:`1.5` through :math:`2` times
the memory's capacity. How did they manage to do this? JVM arguments and virtualisation. By setting the `-Xms` flag of the
JVM to some number around 128M, the Minecraft server will have to constantly ask the JVM, which in turn asks the OS for new
memory as they are required. This is very slow, but maximises profit with margins that would make AWS (Amazon Web Services) weep.

How to Spot a Scammer
~~~~~~~~~~~~~~~~~~~~~

*   **"Unlimited" Everything**: RAM, CPU, and Disk are finite physical resources. Anyone claiming "unlimited" is being deceptive.
*   **No Legal Entity**: Check the footer for a registered company number and address. If it's just a Discord link, walk away.
*   **Free Templates**: If the website looks like a generic $10 template with no custom branding, they aren't invested in their business.

.. seealso::

   * :doc:`summer_hosts`: Our deep dive into identifying bad hosts.
   * :doc:`hall_of_shame`: A list of companies that failed their customers.
