# ns8-euro-office

This is the Euro-Office app for NethServer 8.

## Install

Install via Software center:

  - Add a Software repository pointing to `https://repo.mrmarkuz.com/ns8/updates/`, check out the [repo webpage](https://repo.mrmarkuz.com) how to do it.
  - Install Euro-Office via Software Center

Instantiate the module on CLI with:

    add-module ghcr.io/mrmarkuz/euro-office:latest 1

The output of the command will return the instance name.
Output example:

    {"module_id": "euro-office1", "image_name": "euro-office", "image_url": "ghcr.io/mrmarkuz/euro-office:latest"}

## Configure

The FQDN needs to be configured in the Web UI app settings. The FQDN is required. It should be a unique FQDN that's not already used in your NS8 else Onlyoffice won't be reachable.

## JWT Secret

To get the JWT secret that needs to be configured in client apps like Nextcloud: (in this example the instance is named euro-office1)

    runagent -m euro-office1 grep JWT_SECRET environment

## Nextcloud

- Install the eurooffice app, see https://github.com/Euro-Office/eurooffice-nextcloud#installing-euro-office-app-for-nextcloud-
- Go to Nextcloud administration Eurooffice app settings
- Set the "Office address" that is the FQDN of the Eurooffice app.
- Set the "Secret key" that you got from the previous chapter.

## Use a self signed cert or how to disable the certificate check

Open the Onlyoffice web app in your browser and allow the self-signed certificate to avoid an `ONLYOFFICE cannot be reached. Please contact admin` error in Nextcloud.

In the following examples euro-office6 is used as app instance name, please change it to match your environment.

Edit the environment file and add "USE_UNAUTHORIZED_STORAGE=true":

    runagent -m euro-office1 nano environment

Alternative command to add the environment variable:

    runagent -m euro-office1 bash -c "grep -q USE_UNAUTHORIZED_STORAGE environment || echo USE_UNAUTHORIZED_STORAGE=true >> environment"

Restart euro-office to apply the changes:

    runagent -m euro-office1 systemctl --user restart euro-office-app

## Uninstall

To uninstall the instance:

    remove-module --no-preserve euro-office1
