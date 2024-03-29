# Gitops App and Manifest Example

This is a working example of an applicaiton repo and a manifest repo working in tandem as one CI unit.

The order of events is as follows.

## Code Change

1. A change is made to application code, committed, and pushed to Github, then a PR is made.
2. Upon PR create, Actions does the following:
   * creates a new image tagged with PR & branch head SHA-7
   * opens a PR in the manifest repo against the 'dev' kustomize overlay
3. The manifest repo PR is picked up by an ArgoCD applicationset, which creates a new app based on the kustomize yaml.
4. As new commits are made to the PR branch, new images are created with new PR & branch head SHA-7 tags.
   * the *same manifest repo is used* for each new image created

## Semver Tag

Dev will push a new semver tag to github with the PR branch still checked out.

* this tags the current PR & SHA-7 image
* the manifest repo PR's 'prod' kustomize overlay is updated 

## PR Close

1. Developer closes & merges app PR
   
   * all previous PR & SHA-7 images are deleted
   
   * manifest repo PR is closed & merged to main
   
     * ArgoCD applicationset sees PR closed, so dev app is destroyed
   
     * ArgoCD prod application profile sees a new image version and updates accordingly

## Source

The example [app](https://github.com/evanshortiss/gitops-gh-actions-application) and [manifest](https://github.com/evanshortiss/gitops-gh-actions-manifests) were originally written by [Evan Shortiss](https://github.com/evanshortiss).