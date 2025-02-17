# Continuous Integration (CI)

The GitHub Actions in the directory [`.github/workflows`](https://github.com/Arm-Examples/AWS_MQTT_Demo/tree/main/.github/workflows) are the scripts for the CI tests. These scripts contain detailed comments about each step that is executed.

## GitHub Secrets

[GitHub Secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions) are variables that are set in the [Secret store](../../settings/secrets/actions). This secrets can be read by GitHub
actions but are otherwise not accessible. The following GitHub Secrets need to be added to a repository fork in the [Secret store](../../settings/secrets/actions) to connect a [*AWS IoT Thing*](https://docs.aws.amazon.com/iot/latest/developerguide/iot-moisture-create-thing.html).

GitHub Secret                  | Enables *AWS IoT Thing* Connection
:------------------------------|:---------------------------------------
`CLIENT_CERTIFICATE_PEM`       | Client (device) certificate
`CLIENT_PRIVATE_KEY_PEM`       | Client (device) private key
`IOT_THING_NAME`               | Client  (device) name
`MQTT_BROKER_ENDPOINT`         | MQTT broker host name

## Format of GitHub Secrets

Before entering the secrets into the [Github Secret store](../../settings/secrets/actions) it is necessary to format the GitHub secrets as explained below.

GitHub Secret name             | Original or issued format           | Github Secret Store format
:------------------------------|:------------------------------------|:---------------------------------------
`IOT_THING_NAME`               | Single line string without quotes   | Single line string without quotes i.e.  `myIoT_thing_name`
`MQTT_BROKER_ENDPOINT`         | Single line string without quotes   | Single line string without quotes i.e.  `random-string.abcd.xyz.amazonaws.com`
`CLIENT_CERTIFICATE_PEM`       | Multiline string. See **F1**.       | Single line string with double quotes and additional new-lines. See **F2**.
`MQTT_BROKER_ENDPOINT`         | Multiline string. See **F3**.       | Single line string with double quotes and additional new-lines. See **F4**.

**F1**: The issued Certificate format is a multiline string like:

```txt
-----BEGIN CERTIFICATE-----
::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::==
-----END CERTIFICATE-----
```

**F2**: The expected Certificate format must be a double-quoted singleline string. i.e.

```txt
"-----BEGIN CERTIFICATE-----\n\::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::==\n-----END CERTIFICATE-----\n"
```

**F3**: The issued Private Key format is a multiline string like:

```txt
-----BEGIN RSA PRIVATE KEY-----
::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::
-----RSA PRIVATE KEY-----
```

**F4**: The expected Private Key format must be a double-quoted singleline string. i.e.

```txt
"-----BEGIN RSA PRIVATE KEY-----\n\::::::::::::::::::::::::::::::::::::::::::::::\n-----END RSA PRIVATE KEY-----\n"
```
