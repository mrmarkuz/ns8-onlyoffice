# ns8-onlyoffice

This is the Onlyoffice app for NethServer 8.

## Install

Install via Software center:

  - Add a Software repository pointing to `https://repo.mrmarkuz.com/ns8/updates/`, check out the [repo webpage](https://repo.mrmarkuz.com) how to do it.
  - Install Guacamole via Software Center

Instantiate the module on CLI with:

    add-module ghcr.io/mrmarkuz/onlyoffice:latest 1

The output of the command will return the instance name.
Output example:

    {"module_id": "onlyoffice1", "image_name": "onlyoffice", "image_url": "ghcr.io/mrmarkuz/onlyoffice:latest"}

## Configure

The FQDN needs to be configured in the Web UI app settings. The FQDN is required.

## JWT Secret

To get the JWT secret that needs to be configured in client apps like Nextcloud: (in this example the instance is named onlyoffice1)

    runagent -m onlyoffice1 grep JWT_SECRET environment

## Nextcloud

- Install the ONLYOFFICE app
- Go to Nextcloud administration Onlyoffice app settings
- Set the "Onlyoffice Docs address" that is the FQDN pf the Onlyoffice app.
- Set the "Secret key" that you got from the previous chapter.

## Uninstall

To uninstall the instance:

    remove-module --no-preserve onlyoffice1
