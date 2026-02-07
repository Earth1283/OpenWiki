Creating Your First Server
==========================

.. _installation:

Picking Your Server Software
----------------------------

There are many open and closed sourced Minecraft server software avalible 
for you to chose from that many do not know which to chose. For instance,
there is the obvious choise of `PaperMC <https://papermc.io/downloads/paper>`_,
and the newer options of "performance forks" (we will cover that in a momment)
such as `LeafMC <https://www.leafmc.one/downloads>`_.

Minecraft server software has came a long way since the early 2010s. It went like this:

.. mermaid::

    graph TD
        %% Nodes
        Vanilla[Vanilla - Mojang Official]
        hMod[hMod - Legacy Wrapper]
        CraftBukkit[CraftBukkit - The API Foundation]
        Spigot[Spigot - Performance & Anti-Xray]
        Paper[PaperMC - The Industry Standard]
        Tuinity[Tuinity - Optimized Logic/Starlight]
        Pufferfish[Pufferfish - Enterprise Performance]
        Purpur[PurpurMC - Feature-Rich Customization]
        Leaf[Leaf - Extreme Performance / Unstable]

        %% Evolution Flow
        Vanilla --> hMod
        Vanilla --> CraftBukkit
        hMod -.->|Team Transition| CraftBukkit
        CraftBukkit --> Spigot
        Spigot --> Paper
        Paper --> Tuinity
        Tuinity -->|Merged into| Paper
        Paper --> Pufferfish
        Pufferfish --> Purpur
        Purpur --> Leaf

        %% Styling
        style Vanilla fill:#f9f,stroke:#333,stroke-width:2px
        style Paper fill:#00d2ff,stroke:#000,stroke-width:2px
        style Purpur fill:#b19cd9,stroke:#000,stroke-width:2px
        style Leaf fill:#ff6666,stroke:#800,stroke-width:3px,stroke-dasharray: 5 5

As you can see, the "evolution" of server forks in the past decade or so
has been blazingly fast. This started from the vanilla server.jar, which is
distribtued by Mojang. It is **not advised** for you to use this. Similarly,
old and discontinued forks such as (CraftBukkit) Bukkit are not advised.

At a bare minimum, you should use PaperMC, or, if you feel like using a more configurable
server version, choose PurPurMC. These are the two forks that are regaurded as "most stable"
for modern Minecraft.

.. warning ::
    Unless your hardware is **heavily constrained**, do NOT use Leaf. It is
    not worth the risk