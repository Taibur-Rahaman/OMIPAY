# OMIPAY — Open-Source Payment Automation Platform

<p align="center">
  <img src="branding/omipay-logo.svg" alt="OMIPAY logo" width="320">
  <br><em>Payment automation for businesses and developers</em>
</p>

<p align="center">
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-AGPL--3.0-blue.svg?style=for-the-badge&logo=gnu&logoColor=white" alt="AGPL-3.0 License">
  </a>
  <img src="https://img.shields.io/badge/Status-Educational%20Preview-orange?style=for-the-badge" alt="Educational Preview">
</p>

OMIPAY is an open-source payment automation project intended for learning, evaluation, and development of payment workflows. It is based on the upstream [PipraPay](https://github.com/PipraPay/PipraPay) project and remains subject to the applicable AGPL-3.0 license and upstream notices.

> **Important:** This repository is an educational/development preview. Do not use it to process real customer payments until deployment security, payment-provider approvals, compliance requirements, monitoring, backups, and incident-response procedures have been reviewed and tested.

## Project goals

- Explore payment workflow automation in a self-hosted application.
- Evaluate supported payment connectors and integration patterns.
- Develop and test API, webhook, and plugin integrations.
- Provide a foundation for a properly licensed and secured hosted service.

Actual provider availability and features depend on the code version, configuration, credentials, and provider terms. Verify each integration in a sandbox before relying on it.

## Getting started

1. Review the repository files and the installation instructions supplied with the project.
2. Configure a local development environment using test credentials only.
3. Run the application and validate workflows in a sandbox.
4. Review security settings before exposing any instance to the internet.

Installation details may change as this repository is prepared for OMIPAY. Do not put production secrets, API keys, or customer data into source control.

## Commercial and hosted-service plans

The long-term goal is to evaluate a subscription-based hosted service for businesses in Bangladesh and other markets. This repository does not by itself represent a production-ready or compliant payment service. Any hosted deployment must satisfy the applicable AGPL-3.0 source-code obligations for modified versions used over a network, as well as relevant payment-provider terms and local laws.

## Upstream attribution and license

OMIPAY is based on **PipraPay**. Upstream project: https://github.com/PipraPay/PipraPay

This project is licensed under **GNU Affero General Public License v3.0 (AGPL-3.0)**, subject to the license file and notices included in this repository. Preserve applicable copyright, license, and attribution notices in source distributions and modified versions. For modified versions made available for network interaction, review AGPL-3.0 Section 13 and provide the corresponding source code as required by the license.

- License text: [LICENSE](LICENSE)
- Upstream project: [PipraPay on GitHub](https://github.com/PipraPay/PipraPay)

OMIPAY branding does not imply ownership of upstream code or third-party trademarks.