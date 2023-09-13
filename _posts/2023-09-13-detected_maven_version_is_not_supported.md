---
title: 'quarkus dev and Detected Maven Version'
subtitle: 'mvn wrapper:wrapper'
date: 2023-09-13
excerpt: Failed to execute goal io.quarkus.platform:quarkus-maven-plugin:3.3.2:dev (default-cli) on project... Detected Maven Version (3.6.3)  is not supported
tags: troubleshooting
---

I got the following error running 'quarkus dev' on an older project:

```

Failed to execute goal io.quarkus.platform:quarkus-maven-plugin:3.3.2:dev (default-cli) on project... Detected Maven Version (3.6.3)  is not supported, it must be in [3.8.2,).

```

I should have figured the answer out quickly because I don't even have Maven 3.6.3 on my machine.  I needed to create the Maven wrapper folder, which is easy to do:

```

mvn wrapper:wrapper

```
