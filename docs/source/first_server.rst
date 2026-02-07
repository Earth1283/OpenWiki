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
    not worth running the risk of potential playerdata corrution for performance that
    has yet to proven it's stability.

As a good rule of thumb, always fetch the latest release from the respective source.
There is absolutely no point in, say, fetching release 123 when release 132 is avalible.
New releases often fix security vulnerabilities and dupilication glitches/exploits which older
builds do not cover.

.. tip::
    If you are running a server with a version number higher than `1.9.2`, the server
    would typically make an `eula.txt` file for you to set `eula=false` to `eula=true`.
    
    In order to automate this process (especially if you are on a bare metal VPS), it is
    best if you can run the following bash command:

    .. code-block:: bash
        rm eula.txt; echo "eula=true" > eula.txt

    This command removes the origional eula.txt (in case there was some hanging data), and
    the second part of the command, `echo "eula=true"`, outputs `eula=true` to `STDOUT <https://en.wikipedia.org/wiki/Standard_streams>`_.
    The `>` operator catpures the STDOUT and moves it to a file named `eula.txt`, effectively
    agreeing to the EULA for you.

The following sectinos will explore the nuances of certain server software.

Pros and Cons of PaperMC
------------------------
PaperMC, as the industry standard for so many years, is known for it's reliability, stability, and performance
comapred to previous implementations/versions of the Spigot/Bukkit API. PaperMC tries to implement
vanilla features while maximizing performance.