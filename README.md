# CICD Template

This CICD workflow builds Unity projects on push (to dedicated branches if desired) and publishes them to the App Center and/or the Google Play Store and iOS App Store.

## Resources

This is heavily based off of the GameCI templates [(android)](https://game.ci/docs/github/deployment/android) and [(iOS)](https://game.ci/docs/github/deployment/ios) as well as this YouTube tutorial by [LP Games](https://www.youtube.com/watch?v=M2BZr02uai0) and [this](https://github.com/marketplace/actions/app-center-distribute) Github action for publishing to the App Center. 

## Files

There are several different YAML files that each build and distribute different builds. (Having them seperate was to allow you to customise the triggers and behaviour of individual workflows)

Each is split into 3 jobs: a test runner; the build of the app; and the distribution of the app. The first is independant and could be removed/disabled if not desired. 
The build is created using GameCI's `game-ci/unity-builder@v2`action and is uploaded as an artifact - which can be downloaded. Then it is uploaded to the stores, using [Fastlane](https://fastlane.tools/) for publishing to the Play store and App store, and an independant action linked in the resources for publishing to the App center.
The artifact is then destroyed to save space but this can be removed if you would like to save the artifact (this is the last step of the publishing job)
