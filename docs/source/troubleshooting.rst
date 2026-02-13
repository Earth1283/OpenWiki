The Art of Troubleshooting
==========================

Every server administrator will eventually face a crash, a "lag spike," or a plugin that simply refuses to work. Learning how to diagnose these issues is what separates a "server owner" from a "server administrator."

Reading the Logs
----------------

Your server's console and the `logs/latest.log` file are your most important tools. They tell you exactly what the server is doing—and why it stopped doing it.

.. mermaid::

   graph TD
       Error[Error Occurs] --> Log[Check latest.log]
       Log --> FirstLine[Read FIRST line of Stack Trace]
       FirstLine --> Identify[Identify Plugin Name]
       Identify --> Action{Is it a known plugin?}
       Action -- Yes --> Search[Search GitHub Issues]
       Action -- No --> System[Check Java/OS version]
       
       style FirstLine fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#01579b

.. tip::

   When asking for help online, **never** take a photo of your screen with a phone. Always share your log file using a service like `mclogs <https://mclogs.org/>`_ or `Pastebin <https://pastebin.com/>`_.

Understanding Common Log Patterns
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*   **INFO**: Standard messages. "Player joined," "Server started," etc.
*   **WARN**: Something isn't quite right, but the server can keep running. Often related to outdated plugins or minor configuration errors.
*   **ERROR/SEVERE**: Something has gone wrong. A plugin might have failed to load, or a command might have crashed.
*   **Stack Traces**: These long blocks of text (starting with `at ...`) look scary, but they are just a "map" of the error. Look at the very first line of the trace to find the name of the plugin causing the issue.

Common Error Glossary
~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Common Console Errors
   :widths: 30 70
   :header-rows: 1

   * - Error Name
     - Meaning & Solution
   * - ``java.net.BindException: Address already in use``
     - Another application is already using port 25565. Check if another server is running or change your port in ``server.properties``.
   * - ``java.lang.ClassNotFoundException``
     - A plugin is missing a dependency. Check the plugin's documentation for required "Lib" plugins.
   * - ``java.lang.OutOfMemoryError``
     - The JVM has run out of RAM. Increase your ``-Xmx`` value or find a memory leak using Spark.
   * - ``UnsupportedClassVersionError``
     - You are trying to run a plugin or server jar built for a newer version of Java (e.g., trying to run Java 21 code on Java 17). Update your Java version.

Crash Reports
-------------

If your server stops completely, it will generate a file in the `crash-reports/` folder. This file contains a snapshot of what every part of the server was doing at the exact moment of the crash.

**Key sections to look for:**
*   **Description**: A brief summary of the crash (e.g., `Watching Server`, `Exception in server tick loop`).
*   **Relevant Details**: Tells you which world, coordinates, or entities were involved.

.. warning::

   **JVM Fatal Crashes (hs_err_pid.log)**
   If your server vanishes without a crash report or log entry, check your main folder for a file named ``hs_err_pid<number>.log``. This indicates that the **Java process itself** crashed. This is usually caused by faulty hardware (bad RAM), incompatible drivers, or running out of system memory (OOM Killer on Linux).

Advanced Debugging with Spark
-----------------------------

`Spark <https://spark.lucko.me/>`_ is a powerful performance profiler that comes pre-installed on many modern forks or can be added as a plugin.

.. tab-set::

   .. tab-item:: 📊 CPU Profiling
      :sync: spark-cpu

      Run ``/spark profiler start``, wait 5-10 minutes, then run ``/spark profiler stop``.
      
      *   Open the link provided.
      *   Look for "Large" branches in the tree.
      *   If a plugin name appears at the top of a large branch, it is consuming a significant portion of your CPU.

   .. tab-item:: 🧊 Memory (RAM) Issues
      :sync: spark-mem

      If your server is "hanging" or crashing with `OutOfMemoryError`, run ``/spark heapsummary``.
      
      *   This will show you which parts of the server are holding onto the most RAM.
      *   Common culprits: Large world maps, massive entity counts, or "Memory Leaks" in poorly written plugins.

   .. tab-item:: 📈 TPS & Tick Duration
      :sync: spark-tps

      Run ``/spark tps`` and ``/spark health``.
      
      *   **TPS**: Should be 20.0. Anything lower means the server is lagging.
      *   **MSPT (Milliseconds Per Tick)**: Should be below 50ms. If it hits 50ms, your TPS will drop.

Finding the Culprit: The Binary Search Method
---------------------------------------------

If your server is crashing but you can't figure out which plugin is responsible, use the "Binary Search" method:

.. mermaid::

   graph TD
       Start[Backup Server] -- "Remove 50%" --> Split[Plugin Pool Split]
       Split -- "Test Run" --> Run[Start Server]
       Run -- "Verify Logs" --> Crash{Is it Crashing?}
       Crash -- "Yes" --> HalfA[Problem in Active Set]
       Crash -- "No" --> HalfB[Problem in Removed Set]
       HalfA -- "Iterate" --> Done{Isolate Single?}
       HalfB -- "Iterate" --> Done
       Done -- "No" --> Split
       Done -- "Yes" --> Culprit[Plugin Identified]
       
       style Culprit fill:#f0fdf4,stroke:#166534,stroke-width:2px,color:#166534
       style Start fill:#eff6ff,stroke:#1e40af,color:#1e40af

1.  **Backup your server.**
2.  Remove **half** of your plugins.
3.  Start the server.
4.  Does it still crash?
    *   **Yes**: The problem is in the half you kept.
    *   **No**: The problem is in the half you removed.
5.  Repeat this process with the "bad" half until only one plugin remains.

Reporting Bugs Effectively
--------------------------

When you find a bug in a plugin, reporting it correctly ensures the developer can fix it quickly.

1.  **Search First**: Check the plugin's GitHub Issues or Discord to see if someone else has already reported it.
2.  **Be Specific**: "It doesn't work" is not a bug report.
3.  **Provide Context**:
    *   What version of Minecraft/Paper are you using?
    *   What version of the plugin are you using?
    *   What were you doing when the bug happened?
4.  **Include Logs**: Provide a link to your full log or crash report.

.. seealso::

   * :doc:`optimization`: Learn how to prevent performance issues before they start.
   * :doc:`first_server`: Ensure your Java environment is set up correctly to avoid common startup errors.
