---
title: 'Searching Quarkus Extensions with the Quarkus CLI'
subtitle: 'Hopefully writing this down will make it easier for me to remember the commands'
date: 2023-05-31 00:00:00
excerpt: When using the Quarkus CLI to search for extensions while inside a project directory run, "quarkus ext list -i -s [FUNCTION NAME]"
---

I love the <a href="https://quarkus.io/guides/cli-tooling" target="_blank">Quarkus CLI</a>.  I use to create projects, work with extensions, start Quarkus, build projects.

Working with extensions can be a bit tricky because the (default) output is different when run inside and outside of a project directory.  Running 'quarkus ext ls' from inside of a project directory lists the installed extensions.  Outside of a project directory it lists all the extensions.

While that makes some logical sense, when adding an extension to my project I prefer not to change directories to search for extensions.  The flags for this are:

quarkus ext list -i -s funqy

"-i" means installable
"-s" is search