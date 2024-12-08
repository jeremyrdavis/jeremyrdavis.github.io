---
title: 'GitHub Action for Quarkus'
subtitle: 'A GitHub Action that builds your app as a container and pushes it to Docker'
date: 2024-12-01
excerpt: A GitHub Action that builds a Quarkus app, creates a container, and pushes to Dockerhub
---

GitHub Actions are a fantastic time saver.  I've been using them for a while and have recently had the chance to start expanding functionality.  Building and pushing Docker containers is a great place to start because I do that all the time.

If you are familiar with GitHub Actions most of the file is straightforward. If you *aren't* familiar with GitHub Actions, [start here](https://docs.github.com/en/actions/writing-workflows/quickstart).

In lines 22-40 the Maven artifactId and version are stored as variables for the build:

```yaml

      - name: Get artifactId from pom.xml
        id: get_artifactId
        run: echo "::set-output name=artifactId::$(mvn help:evaluate -Dexpression=project.artifactId -q -DforceStdout)"

      - name: Expose artifactId as an output
        run: echo "POM_ARTIFACT=${{ steps.get_artifactId.outputs.artifactId }}" >> $GITHUB_ENV

      - name: Print artifactId
        run: echo $POM_ARTIFACT

      - name: Get version from pom.xml
        id: get_version
        run: echo "::set-output name=version::$(mvn help:evaluate -Dexpression=project.version -q -DforceStdout)"

      - name: Expose version as an output
        run: echo "POM_VERSION=${{ steps.get_version.outputs.version }}" >> $GITHUB_ENV

      - name: Print version
        run: echo $POM_VERSION

```

The "Get artifact/version from pom.xml" steps pull the values out of the pom.xml and set them into the environment.  The "Print artifactId/version" is just logging.

The Action uses your Docker username to tag the image:

```yaml

   - name: Build Docker image
        run: docker build --file src/main/docker/Dockerfile.jvm -t ${{ secrets.DOCKERHUB_USERNAME }}/${POM_ARTIFACT}:${POM_VERSION} -t ${{ secrets.DOCKERHUB_USERNAME }}/${POM_ARTIFACT}:latest .
```

The push to Dockerub requires your Docker username and a token.

```yaml

      - name: Push Docker image
        run: |
          echo ${{ secrets.DOCKERHUB_TOKEN }} | docker login -u ${{ secrets.DOCKERHUB_USERNAME }} --password-stdin
          docker push ${{ secrets.DOCKERHUB_USERNAME }}/${POM_ARTIFACT}:${POM_VERSION}

```

Your Dockerhub username and token needs to be set in "Settings > Secrets and variables > Actions."  There is a screenshot in the repo's [README.md](https://github.com/jeremyrdavis/a-github-action-for-quarkus) of where to find these settings.

