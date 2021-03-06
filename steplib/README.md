<h1 align="center"><img src="https://app.bitrise.io/app/a0bac497f75e1490/status.svg?token=A3abbQcGjDvqyzGUkdVukw&branch=master" alt="Latest Version"></img> StepLib</h1>

<h4 align="center">Bitrise StepLib is a versioned collection of the Bitrise Steps.<br>The visual representation of the StepLib can be found here: <a href="https://www.bitrise.io/integrations/steps">Integrations</a></h4>

<p align="center">
Some of our sub-sites if you are new to Bitrise and want read more about Steps and our products:
<br>
  <a href="https://devcenter.bitrise.io">devcenter.bitrise.io</a> •
  <a href="https://discuss.bitrise.io">discuss.bitrise.io</a> •
  <a href="https://blog.bitrise.io">blog.bitrise.io</a>
</p>

# Structure

When you have a Step repository you can share that to our StepLib so it will become visible in our Workflow Editor and in the `bitrise.yml`. When you share your step we store a copy of your `step.yml` with a very little change because we need to store where your currently shared step version source is available. This is the reason we request a re-share if you made any changes to the current version of the step.

#### `step.yml`s
```txt
/steps/<step-id>/<step-version>/step.yml
```
> `<step-id>` is to be able to identfy a step for example in `bitrise.yml`. For example: `- step-id@version: {}`

#### Step icon
```txt
/steps/<step-id>/assets/icon.svg
```

#### Deprecation note
```txt
/steps/<step-id>/step-info.yml
```
> With an example content:
>```yaml
>removal_date: "2018-09-20"
>deprecate_notes: |
>  This step is deprecated, some 3rd party service is now abandoned. Please use "another" step instead.
>```


# Contribution

## Requirements

- The tag created for a step version in your repository cannot be re-used/moved to another commit hash.
    > This is because we use the tag as the version and the commit hash also stored to the version so this way we can make sure that a source is surely matching the version.
    ![Tag](assets/tag.png)
- You need to read our [Step Development Guideline](https://github.com/bitrise-io/bitrise/blob/master/_docs/step-development-guideline.md).
- In the source reporitory must have a test which can be run with `bitrise run test` so we can test your Step under the PR review.
- Our Step auditor must pass. To check it yourself run our stepman tool in in your repository.
    > stepman audit --step-yml ./step.yml
    
    _Visit our [stepman](https://github.com/bitrise-io/stepman) tool's site to read more._
- You need to read and accept the [Abandoned Step policy](#abandoned-step-policy)

## Share your own Step

You can share your Step or step version with the [bitrise CLI](https://github.com/bitrise-io/bitrise). If you use the `bitrise.yml` included in this repository, all you have to do is:

1. In your Terminal / Command Line `cd` into this directory (where the `bitrise.yml` of the step is located)
1. Run: `bitrise run test` to test the step
1. Run: `bitrise run audit-this-step` to audit the `step.yml`
1. Check the `share-this-step` workflow in the `bitrise.yml`, and fill out the
   `envs` if you haven't done so already (don't forget to bump the version number if this is an update
   of your step!)
1. Then run: `bitrise run share-this-step` to share the step (version) you specified in the `envs`
1. Send the Pull Request, as described in the logs of `bitrise run share-this-step`


# Abandoned Step policy

We try to keep this Step Library up-to-date and active. Steps shared in this collection have to be actively maintained to receive fixes / updates when required (e.g. security issue fixes or general usability fixes).

**If you're a Step maintainer** you're not required to accept every Pull Request sent to your Step **but you should be reachable within a reasonable timeframe**. If we try to contact you several times regarding an important fix/update in your Step and you refuse to answer for several weeks *we might deprecate, remove or replace your Step* in the collection. Abandoned Steps can be a threat for those who use it, please keep this in mind if you decide to share your Step with others!

**If you shared a Step but you're no longer able to or you don't want to maintain it** please create a GitHub issue in this repository (https://github.com/bitrise-io/bitrise-steplib).

**If you're a user of a Step which has critical (security or functionality) issues** please create a ticket in the Step's Issue Tracker (every Step declares the preferred way of reporting issues with the `support_url` attribute - [see](https://github.com/bitrise-io/bitrise-steplib/blob/master/steps/activate-ssh-key/3.1.0/step.yml#L15)) first. If you don't get a response from the Step's maintainer for an extended period (reasonably, in general, for more than a couple of weeks) please create a GitHub issue in this repository (https://github.com/bitrise-io/bitrise-steplib) and we'll try to resolve the issue, following the Abandoned Step policy. *Please be patient* and keep in mind that everyone who contribute to this collection does that with an intention to help You by providing a Step for you to use, don't be rude to Step maintainers!