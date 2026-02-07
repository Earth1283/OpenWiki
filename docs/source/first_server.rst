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

    .. highlight::bash:
        rm eula.txt; 

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

PaperMC in on itself is very configurable, allowing you access to Bukkit, Spigot, and Paper's configuration
files. You can tweak mob spawn times, item despawn times, and even configure one of the
best and most performant anti-xray features on planet Earth.

The obvious disadvantage of PaperMC is that their core development team believes that PaperMC
should remain as closely vanilla-ish as possible, often rejecting creative options that PurPurMC accepts.

Pros and Cons of PurPurMC
-------------------------
PurPurMC, as a fork of Pufferfish (in turn, a fork of Paper), offers more optimizations and creative configuration options
when compared to traditional Paper. PurPur is famous for their `purpur.yml` that is, though thousands of lines long,
offers more configurability than any amount of default PaperMC configurations could offer.

PurPur, being a downstream fork from Pufferfish, benefits from Pufferfish's optimizations, which compounds
towards their further optimizations in purpur.yml.

The downside is clear. PurPurMC traded configurability with ease of use. People get scared off by Purpur's
thousand-line long `purpur.yml` without deriving its complete value, resulting in an ultimate loss
of potential features presented by PurPur.

Setting up your first server
----------------------------
.. warning::
    This guide assumes that you have access to the JVM flags of your instance. If you are unable
    to edit them yourself, you should ask your server hosting provider via a ticket. Legiemate hosts
    typically allow these requests, while summer hosts that oversell their nodes typically deny such requests,
    as these flags make the JVM allocate memory more efficiencly. More on this at a later date.

Begin with downloading the server binary (aka, server.jar) from your vendor, be it Paper or Purpur.

Then place it inside your server directory, and then create a file named `eula.txt` with the following content:

.. codeblock::
    eula=true

This agrees to the Mojang EULA before the server starts. Then, configure your startup flags.
If you are on a bare metal VPS, do **NOT** allocate all your avalible memory to the Java Heap. This will
lead to your operating system running out of memory and your server crashing.
