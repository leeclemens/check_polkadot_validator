# Checks for Polkadot/Kusama Validators

## Status

![License](https://img.shields.io/github/license/leeclemens/check_polkadot_validator)
![Issues](https://img.shields.io/github/issues-raw/leeclemens/check_polkadot_validator)
![Pull Requests](https://img.shields.io/github/issues-pr/leeclemens/check_polkadot_validator)

### main

![Linting main](https://github.com/leeclemens/check_polkadot_validator/actions/workflows/linters.yml/badge.svg?branch=main)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/54641d02ffdd4a819cfd221b8a3e6c86?branch=main)](https://app.codacy.com/gh/leeclemens/check_polkadot_validator/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)

### develop

![Linting develop](https://github.com/leeclemens/check_polkadot_validator/actions/workflows/linters.yml/badge.svg?branch=develop)
[![Codacy Badge develop](https://api.codacy.com/project/badge/Grade/54641d02ffdd4a819cfd221b8a3e6c86?branch=develop)](https://app.codacy.com/gh/leeclemens/check_polkadot_validator?utm_source=github.com&utm_medium=referral&utm_content=leeclemens/check_polkadot_validator&utm_campaign=Badge_Grade)

## Description

A collection of checks for your validators that are Nagios/Icinga2 compatible,
or can be run in an idempotent manner. The primary goal was to achieve an
idempotent health check for determining the status of a validator.

Some challenges include testing for the advancement in block height.
This infers passage of time, so it is difficult to check idempotently.

## Requirements

* Python 3.8+
* PyPI websockets package
  * pip install websockets
* Debian/Ubuntu, RedHat/CentOS/Fedora package
  * python3-websockets

## Check Validator is Active

### check_polkadot_validator_active

Perform a series of checks to confirm the validator is "active". Some checks include:

* Currently syncing
* Number of peers
* Block height distance is too great
* Block numbers are not increasing over time

#### Example

```bash
check_polkadot_validator_active -s localhost -p 9944 \
  --min-peers 5 \
  --max-distance-warn 5 \
  --max-distance-crit 8 \
  --best-timeout 14 \
  --finalized-timeout 28
```
