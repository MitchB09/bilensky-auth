# Bilensky Auth (PHP)
https://home.bilensky.ca

Personal home page and testing ground for vite apps


## Infrastructure

To build the AWS SAM template first execute the following to compile template.yaml:

```bash
sam build
sam deploy --guided
```

Deploying Infra to dev environment

```bash
sam deploy --config-file samconfig.toml
```

Deploying to Prod

```bash
sam deploy --config-file samconfig.toml --config-env prod
```

