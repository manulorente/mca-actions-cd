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

[**Workflow 1 - Unit test and API rest test for features**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd/actions/runs/5316790062)  

[**Workflow 2 - All tests when commit into develop branch**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd/actions/runs/5317225235)  

Generating below artifacts:  

[*DockerHub artifact 1*](https://hub.docker.com/layers/manloralm/books-reviewer/dev/images/sha256-fa259eb234a63d4e70251affea480b711d6f6cf246edb79310c1aef0b7b17a98?context=repo)  

[*DockerHub artifact 2*](https://hub.docker.com/layers/manloralm/books-reviewer/0.3.0-SNAPSHOT-dev/images/sha256-fa259eb234a63d4e70251affea480b711d6f6cf246edb79310c1aef0b7b17a98?context=repo)  

[*GitHub packages artifact 1*](https://github.com/users/manulorente/packages/container/books-reviewer/102896973?tag=dev)  

[*GitHub packages artifact 2*](https://github.com/users/manulorente/packages/container/books-reviewer/102896973?tag=0.3.0-SNAPSHOT-dev)  

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

[**Workflow 4 - All unit and rest tests when PR on develop & push on release**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd/actions/runs/5317114879)

Generating below artifacts:  

[*DockerHub artifact*](https://hub.docker.com/layers/manloralm/books-reviewer/0.2.0-rc1/images/sha256-c3541cf70a4a670c27ec9f3419138ee1baa57ad4ce8ef0c2ec575d3483c3e5d6?context=repo)  

[*GitHub packages artifact*](https://github.com/users/manulorente/packages/container/books-reviewer/102889728?tag=0.2.0-rc1)

Once the pull-request is approved, the workflow will be triggered:

[**Workflow 5 - All unit tests and rest tests on commit into production**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd/actions/runs/5317115185)

Generating below latest artifacts:  

[*DockerHub artifact*](https://hub.docker.com/layers/manloralm/books-reviewer/latest/images/sha256-e5c7cb307f4dee4f1d0dd642944c32ce33cadbcc7ef1e4debb6d90072b46e87c?context=repo)  

[*GitHub packages artifact*](https://github.com/users/manulorente/packages/container/books-reviewer/102890800?tag=latest)

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

[**Workflow 3 - Nightly workflow**](https://github.com/manulorente/mca-4.2-manuel.lorentea-juanangel.garridol-2023-cd/actions/runs/5317825591)  

Generating below artifacts:  

[*DockerHub artifact 1*](https://hub.docker.com/layers/manloralm/books-reviewer/20230620.022043-nightly/images/sha256-fa259eb234a63d4e70251affea480b711d6f6cf246edb79310c1aef0b7b17a98?context=repo)  

[*DockerHub artifact 2*](https://hub.docker.com/layers/manloralm/books-reviewer/nightly/images/sha256-fa259eb234a63d4e70251affea480b711d6f6cf246edb79310c1aef0b7b17a98?context=repo)  

[*GitHub packages artifact 1*](https://github.com/users/manulorente/packages/container/books-reviewer/102896973?tag=20230620.022043-nightly)  

[*GitHub packages artifact 2*](https://github.com/users/manulorente/packages/container/books-reviewer/102896973?tag=nightly)  
