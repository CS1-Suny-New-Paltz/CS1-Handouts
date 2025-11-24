# Continuous Integration

## Intro to Version Control

Single main branch -> undo/redo across files as a whole
Enforce certain things -> feature branch + pull request
Not covered: merge conflicts, forking a repo, branches off branches

Specific implementation: Git, but there are others

## Enforce Certain Things = Continuous Integration

Specific implementation: Github Actions, but there are others
Basic yml workflow file (review: Javadoc equivalent, sample code/template equivalent)
Autograder uses gradle, configured with build.gradle (no major details, just point out where 'test' is specified)
  Gradle is self-contained, no need to install it
  Can be copied to future projects if you want
