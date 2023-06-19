# CI/CD Assignment 02

Authors: Manuel Lorente Almán y Juan Ángel garrido Lupiañez

[**Repository**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd)

## GitFlow development

Once workflows are defined, we can start developing our application. We will use GitFlow as a branching model. This model is based on two main branches with infinite life:

```sh
    git flow init -d
```

Push changes to develop branch to trigger the workflow:

```sh
    git push --set-upstream origin develop
```

Create new feature branch:

```sh
    git flow feature start break-lines
```  

Modify version in pom.xml file and add functionality:

```sh
    <version>0.2.0-SNAPSHOT</version>
```  

Commit changes and finish feature branch:

```sh
    git add pom.xml
    git add src/test/java/es/urjc/code/daw/library/unitary/LineBreakerUnitaryTest.java 
    git add src/main/java/es/urjc/code/daw/library/book/LineBreaker.java
    git commit -m "Add line breaker tests"
    git push --set-upstream origin feature/break-lines
    git add src/main/java/es/urjc/code/daw/library/book/BookService.java
    git commit -m "Add line breaker functionality"
    git push --set-upstream origin feature/break-lines
    git flow feature finish -k break-lines
```  

A pull-request will be created to merge the release branch into master. Once the pull-request is approved, the workflow will be triggered.

[**Workflow 1 - Unit test and API rest test for features**]()

[**Workflow 2 - All tests when commit into develop branch**]()

Generating below artifacts:
[*DockerHub artifact 1*]()
[*DockerHub artifact 2*]()
[*GitHub packages artifact 1*]()
[*GitHub packages artifact 2*]()

Init a new release branch:

```sh
    git checkout develop
    git pull
    git flow release start 0.2.0
```

Modify version in pom.xml file and prepare release removing SNAPSHOT:

```xml
    <version>0.2.0</version>
```

Commit changes and finish release branch:

```sh
    git add pom.xml
    git commit -m "Prepare release 0.2.0"
    git push --set-upstream origin release/0.2.0
```

Below we can see the workflow triggered when the release branch is created:

[**Workflow 4 - All unit and rest tests when PR on develop & push on release**]()

Generating below artifacts:
[*DockerHub artifact*]()
[*GitHub packages artifact*]()

Once the pull-request is approved, the workflow will be triggered:

[**Workflow 5 - All unit tests and rest tests on commit into production**]()

Generating below latest artifacts:
[*DockerHub artifact*]()
[*GitHub packages artifact*]()

Merge release to develop:

```sh
    git checkout develop
    git pull
    git merge release/0.2.0
    git push
    git flow release finish -k 0.2.0
```

Modify version in pom.xml file:

```xml
    <version>0.3.0-SNAPSHOT</version>
```

Commit changes and push to develop:

```sh
    git add pom.xml
    git commit -m "Prepare next development iteration"
    git push --set-upstream origin develop
```

## Nightly build

[**Workflow 3 - Nightly workflow**]()
