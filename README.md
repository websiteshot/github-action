# Websiteshot Github Action

<hr />

<div align="center">
    <a href="https://websiteshot.app/">
        <img src="https://websiteshot-docs.s3.eu-central-1.amazonaws.com/logopublicsmall.png" width="100">
    </a>
</div>

<div align="center">
<p>Never spend time again to create awesome screenshots of your websites.</p>
</div>

<div align="center">
<a style="margin: 1em;" href="https://websiteshot.app">Website</a> | <a style="margin: 1em;" href="https://console.websiteshot.app">Console</a> | <a style="margin: 1em;" href="https://github.com/websiteshot/community/discussions">Community</a> | <a style="margin: 1em;" href="https://docs.websiteshot.app">Documentation</a>
</div>

<hr />

This Github action creates a new screenshot job via Websiteshot. Prerequisite for the use is an account at Websiteshot.

## Usage

Name of Action: `websiteshot/github-action`

Mandatory Environment Variables:

- `PROJECT_ID`: The associated Websiteshot project in which the screenshots are created.
- `API_KEY`: Your Websiteshot API Key

One of those Environment Variables must be set:

- `URLS`: URLs für Screenshot creation in `JSON` Format (Array of [url-config](https://docs.websiteshot.app/docs/api/types/url-config))
- `TEMPLATE_ID`: Template Id of Template that should be used

Optional Parameters:

- `SCHEDULE_TS`: Timestamp when to trigger the Screenshot Job
- `SCHEDULE_UNIT` and `SCHEDULE_VALUE`: Instead of a timestamp you can specify a relative description from now on, like `15m` that will be translated into a timestamp in 15 minutes.

This Github action uses Websiteshot's [NodeJS client](https://github.com/websiteshot/nodejs-client) to trigger screenshot jobs.

## Example

An example configuration looks like this:

```yaml
name: Publish

on: [push]

jobs:
  create-screenshot:
    runs-on: ubuntu-latest
    name: 'Schedule Screenshot Creation'
    steps:
      - uses: websiteshot/github-action@main
        env:
          PROJECT_ID: ${{ secrets.PROJECT_ID }}
          API_KEY: ${{ secrets.API_KEY }}
          URLS: '[{"url": "https://websiteshot.app", "name": "Websiteshot"}]'
          SCHEDULE_UNIT: 'm'
          SCHEDULE_VALUE: '5'
```

Or if you want to execute a Job via Template:

```yaml
name: Publish

on: [push]

jobs:
  create-screenshot:
    runs-on: ubuntu-latest
    name: 'Schedule Screenshot Creation via Template'
    steps:
      - uses: websiteshot/github-action@main
        env:
          PROJECT_ID: ${{ secrets.PROJECT_ID }}
          API_KEY: ${{ secrets.API_KEY }}
          TEMPLATE_ID: 'abcdef-ghi...'
```
