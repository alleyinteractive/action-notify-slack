# Run PHP Tests Action

This GitHub Action takes the status and webhook URL from a previous job and sends a notification to a Slack webhook about the status of the job.

## Usage

Example usage in a workflow:

```yaml
name: Deploy production

on:
  push:
    branches:
      - production

jobs:
  build_and_deploy:
    # ... your build and deploy steps here

  notify_slack:
    needs: build_and_deploy
    runs-on: ubuntu-latest
    if: always() # Ensures notification regardless of build outcome
    steps:
      - name: Notify Slack
        uses: alleyinteractive/action-notify-slack@main
        with:
          status: ${{ needs.build_and_deploy.result }}
          webhook_url: ${{ secrets.SLACK_WEBHOOK_URL }}

```

## Inputs

> Specify using `with` keyword.

### `status`

- Provide the status for the Slack notification (e.g. `success`, `failure`, `cancelled`).
- Accepts a string.
- Required: `true`

### `SLACK_WEBHOOK_URL`

- The Slack webhook URL to send the notification to.
- Accepts a string.
- Required: `true`


## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed
recently.

## Credits

This project is actively maintained by [Alley
Interactive](https://github.com/alleyinteractive).

- [Ben Bolton](https://github.com/benpbolton)
- [All Contributors](../../contributors)

## License

The GNU General Public License (GPL) license. Please see [License File](LICENSE)
for more information.
