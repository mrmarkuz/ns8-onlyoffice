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

The FQDN needs to be configured in the Web UI app settings. The FQDN is required. It should be a unique FQDN that's not already used in your NS8 else Euro Office won't be reachable.

## JWT Secret

To get the JWT secret that needs to be configured in client apps like Nextcloud: (in this example the instance is named euro-office1)

    runagent -m euro-office1 grep JWT_SECRET environment

## Nextcloud

- Install the Nextcloud Office 11.0.0 app 
- Go to Nextcloud administration Nextcloud Office app settings
- Set the "Nextcloud Office address" that is the FQDN of the Eurooffice app like `https://eurooffice.domain.tld`
- Set the "Secret key" that you got from the previous chapter

## Fetch documents from a private IP

If Nextcloud resolves to a private IP an environment variable needs to be added.

In the following examples euro-office1 is used as app instance name, please change it to match your environment.

Edit the environment file and add "ALLOW_PRIVATE_IP_ADDRESS=true":

    runagent -m euro-office1 nano environment

Alternative command to add the environment variable:

    runagent -m euro-office1 bash -c "grep -q ALLOW_PRIVATE_IP_ADDRESS environment || echo ALLOW_PRIVATE_IP_ADDRESS=true >> environment"

Restart euro-office to apply the changes:

    runagent -m euro-office1 systemctl --user restart euro-office-app

## Uninstall

To uninstall the instance:

    remove-module --no-preserve euro-office1
