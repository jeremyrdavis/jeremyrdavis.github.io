---
title: 'Quarkus Dev Mode Can't Find Docker'
subtitle: 'Previous attempts to find a Docker environment failed. Will not retry.'
date: 2023-06-04 00:00:00
excerpt: All of a sudden Quarkus can't find Docker or Podman
tags: Quarkus, development, troubleshooting, debugging
---

#### tl;dr

/var/run/docker.sock disappeared

####  Quarkus Dev Mode Couldn't Find Docker

I created a project with Quarkus 3.1.0.Final, which had just dropped, fired up dev mode and got a stack trace (see below.)

I didn't find much searching for the error so I checked Docker Desktop's Settings.  In Settings -> Advanced there is a checkbox to enable the creation of /var/run/docker.sock so that other apps can connect.  The box was checked, but 
"ls -a /var/run | grep docker" didn't show a docker.sock.  Turning off the permission, restarting, turning it back on, and restarting fixed it.


```

java.lang.RuntimeException: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
	[error]: Build step io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor#launchDatabases threw an exception: java.lang.RuntimeException: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:362)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.launchDatabases(DevServicesDatasourceProcessor.java:140)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:568)
	at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:909)
	at io.quarkus.builder.BuildContext.run(BuildContext.java:282)
	at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
	at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2513)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1538)
	at java.base/java.lang.Thread.run(Thread.java:833)
	at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at org.testcontainers.dockerclient.DockerClientProviderStrategy.getFirstValidStrategy(DockerClientProviderStrategy.java:212)
	at org.testcontainers.DockerClientFactory.getOrInitializeStrategy(DockerClientFactory.java:150)
	at org.testcontainers.DockerClientFactory.client(DockerClientFactory.java:186)
	at org.testcontainers.DockerClientFactory$1.getDockerClient(DockerClientFactory.java:104)
	at com.github.dockerjava.api.DockerClientDelegate.authConfig(DockerClientDelegate.java:109)
	at org.testcontainers.containers.GenericContainer.start(GenericContainer.java:321)
	at io.quarkus.devservices.postgresql.deployment.PostgresqlDevServicesProcessor$1.startDatabase(PostgresqlDevServicesProcessor.java:69)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:290)
	... 12 more

	at io.quarkus.runner.bootstrap.AugmentActionImpl.runAugment(AugmentActionImpl.java:335)
	at io.quarkus.runner.bootstrap.AugmentActionImpl.createInitialRuntimeApplication(AugmentActionImpl.java:252)
	at io.quarkus.runner.bootstrap.AugmentActionImpl.createInitialRuntimeApplication(AugmentActionImpl.java:60)
	at io.quarkus.deployment.dev.IsolatedDevModeMain.firstStart(IsolatedDevModeMain.java:86)
	at io.quarkus.deployment.dev.IsolatedDevModeMain.accept(IsolatedDevModeMain.java:447)
	at io.quarkus.deployment.dev.IsolatedDevModeMain.accept(IsolatedDevModeMain.java:59)
	at io.quarkus.bootstrap.app.CuratedApplication.runInCl(CuratedApplication.java:138)
	at io.quarkus.bootstrap.app.CuratedApplication.runInAugmentClassLoader(CuratedApplication.java:93)
	at io.quarkus.deployment.dev.DevModeMain.start(DevModeMain.java:131)
	at io.quarkus.deployment.dev.DevModeMain.main(DevModeMain.java:62)
Caused by: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
	[error]: Build step io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor#launchDatabases threw an exception: java.lang.RuntimeException: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:362)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.launchDatabases(DevServicesDatasourceProcessor.java:140)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:568)
	at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:909)
	at io.quarkus.builder.BuildContext.run(BuildContext.java:282)
	at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
	at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2513)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1538)
	at java.base/java.lang.Thread.run(Thread.java:833)
	at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at org.testcontainers.dockerclient.DockerClientProviderStrategy.getFirstValidStrategy(DockerClientProviderStrategy.java:212)
	at org.testcontainers.DockerClientFactory.getOrInitializeStrategy(DockerClientFactory.java:150)
	at org.testcontainers.DockerClientFactory.client(DockerClientFactory.java:186)
	at org.testcontainers.DockerClientFactory$1.getDockerClient(DockerClientFactory.java:104)
	at com.github.dockerjava.api.DockerClientDelegate.authConfig(DockerClientDelegate.java:109)
	at org.testcontainers.containers.GenericContainer.start(GenericContainer.java:321)
	at io.quarkus.devservices.postgresql.deployment.PostgresqlDevServicesProcessor$1.startDatabase(PostgresqlDevServicesProcessor.java:69)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:290)
	... 12 more

	at io.quarkus.builder.Execution.run(Execution.java:123)
	at io.quarkus.builder.BuildExecutionBuilder.execute(BuildExecutionBuilder.java:79)
	at io.quarkus.deployment.QuarkusAugmentor.run(QuarkusAugmentor.java:160)
	at io.quarkus.runner.bootstrap.AugmentActionImpl.runAugment(AugmentActionImpl.java:331)
	... 9 more
Caused by: java.lang.RuntimeException: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:362)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.launchDatabases(DevServicesDatasourceProcessor.java:140)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:568)
	at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:909)
	at io.quarkus.builder.BuildContext.run(BuildContext.java:282)
	at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
	at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2513)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1538)
	at java.base/java.lang.Thread.run(Thread.java:833)
	at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: java.lang.IllegalStateException: Previous attempts to find a Docker environment failed. Will not retry. Please see logs and check configuration
	at org.testcontainers.dockerclient.DockerClientProviderStrategy.getFirstValidStrategy(DockerClientProviderStrategy.java:212)
	at org.testcontainers.DockerClientFactory.getOrInitializeS(DockerClientFactory.java:150)
	at org.testcontainers.DockerClientFactory.client(DockerClientFactory.java:186)
	at org.testcontainers.DockerClientFactory$1.getDockerClient(DockerClientFactory.java:104)
	at com.github.dockerjava.api.DockerClientDelegate.authConfig(DockerClientDelegate.java:109)
	at org.testcontainers.containers.GenericContainer.start(GenericContainer.java:321)
	at io.quarkus.devservices.postgresql.deployment.PostgresqlDevServicesProcessor$1.startDatabase(PostgresqlDevServicesProcessor.java:69)
	at io.quarkus.datasource.deployment.devservices.DevServicesDatasourceProcessor.startDevDb(DevServicesDatasourceProcessor.java:290)
	... 12 more

```