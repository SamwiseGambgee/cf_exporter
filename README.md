# Cloud Foundry Prometheus Exporter [![Build Status](https://travis-ci.org/cloudfoundry-community/cf_exporter.png)](https://travis-ci.org/cloudfoundry-community/cf_exporter)

A [Prometheus][prometheus] exporter for [Cloud Foundry][cloudfoundry] administrative information. Please refer to the [FAQ][faq] for general questions about this exporter.

## Architecture overview

![](https://cdn.rawgit.com/cloudfoundry-community/cf_exporter/master/architecture/architecture.svg)

## Installation

### Binaries

Download the already existing [binaries][binaries] for your platform:

```bash
$ ./cf_exporter <flags>
```

### From source

Using the standard `go install` (you must have [Go][golang] already installed in your local machine):

```bash
$ go install github.com/cloudfoundry-community/cf_exporter
$ cf_exporter <flags>
```

### Cloud Foundry

The exporter can be deployed to an already existing [Cloud Foundry][cloudfoundry] environment:

```bash
$ git clone https://github.com/cloudfoundry-community/cf_exporter.git
$ cd cf_exporter
```

Modify the included [application manifest file][manifest] to include your Cloud Foundry properties. Then you can push the exporter to your Cloud Foundry environment:

```bash
$ cf push
```

### BOSH

This exporter can be deployed using the [Prometheus BOSH Release][prometheus-boshrelease].

## Usage

### Flags

| Flag / Environment Variable | Required | Default | Description |
| --------------------------- | -------- | ------- | ----------- |
| `cf.api_url`<br />`CF_EXPORTER_CF_API_URL` | Yes | | Cloud Foundry API URL |
| `cf.username`<br />`CF_EXPORTER_CF_USERNAME` | Yes | | Cloud Foundry Username (must be an `administrator` user |
| `cf.password`<br />`CF_EXPORTER_CF_PASSWORD` | Yes | | Cloud Foundry Password |
| `filter.collectors`<br />`CF_EXPORTER_FILTER_COLLECTORS` | No | | Comma separated collectors to filter (`Applications`, `Organizations`, `Services`, `Spaces`) |
| `metrics.namespace`<br />`CF_EXPORTER_METRICS_NAMESPACE` | No | `cf` | Metrics Namespace |
| `skip-ssl-verify`<br />`CF_EXPORTER_SKIP_SSL_VERIFY` | No | `false` | Disable SSL Verify |
| `web.listen-address`<br />`CF_EXPORTER_WEB_LISTEN_ADDRESS` | No | `:9193` | Address to listen on for web interface and telemetry |
| `web.telemetry-path`<br />`CF_EXPORTER_WEB_TELEMETRY_PATH` | No | `/metrics` | Path under which to expose Prometheus metrics |

### Metrics

The exporter returns the following `Applications` metrics:

| Metric | Description | Labels |
| ------ | ----------- | ------ |
| *metrics.namespace*_application_info | Labeled Cloud Foundry Application information with a constant `1` value | `application_id`, `application_name`, `space_id`, `space_name`, `organization_id`, `organization_name` |
| *metrics.namespace*_applications_total | Total number of Cloud Foundry Applications | |
| *metrics.namespace*_last_applications_scrape_error | Whether the last scrape of Applications metrics from Cloud Foundry resulted in an error (`1` for error, `0` for success) | |
| *metrics.namespace*_last_applications_scrape_timestamp | Number of seconds since 1970 since last scrape of Applications metrics from Cloud Foundry | |
| *metrics.namespace*_last_applications_scrape_duration_seconds | Duration of the last scrape of Applications metrics from Cloud Foundry | |

The exporter returns the following `Organizations` metrics:

| Metric | Description | Labels |
| ------ | ----------- | ------ |
| *metrics.namespace*_organization_info | Labeled Cloud Foundry Organization information with a constant `1` value | `organization_id`, `organization_name` |
| *metrics.namespace*_organizations_total | Total number of Cloud Foundry Organizations | |
| *metrics.namespace*_last_organizations_scrape_error | Whether the last scrape of Organizations metrics from Cloud Foundry resulted in an error (`1` for error, `0` for success) | |
| *metrics.namespace*_last_organizations_scrape_timestamp | Number of seconds since 1970 since last scrape of Organizations metrics from Cloud Foundry | |
| *metrics.namespace*_last_organizations_scrape_duration_seconds | Duration of the last scrape of Organizations metrics from Cloud Foundry | |

The exporter returns the following `Services` metrics:

| Metric | Description | Labels |
| ------ | ----------- | ------ |
| *metrics.namespace*_service_info | Labeled Cloud Foundry Service information with a constant `1` value | `service_id`, `service_label` |
| *metrics.namespace*_services_total | Total number of Cloud Foundry Services | |
| *metrics.namespace*_last_services_scrape_error | Whether the last scrape of Services metrics from Cloud Foundry resulted in an error (`1` for error, `0` for success) | |
| *metrics.namespace*_last_services_scrape_timestamp | Number of seconds since 1970 since last scrape of Services metrics from Cloud Foundry | |
| *metrics.namespace*_last_services_scrape_duration_seconds | Duration of the last scrape of Services metrics from Cloud Foundry | |

The exporter returns the following `Spaces` metrics:

| Metric | Description | Labels |
| ------ | ----------- | ------ |
| *metrics.namespace*_space_info | Labeled Cloud Foundry Space information with a constant `1` value | `space_id`, `space_name` |
| *metrics.namespace*_spaces_total | Total number of Cloud Foundry Spaces | |
| *metrics.namespace*_last_spaces_scrape_error | Whether the last scrape of Spaces metrics from Cloud Foundry resulted in an error (`1` for error, `0` for success) | |
| *metrics.namespace*_last_spaces_scrape_timestamp | Number of seconds since 1970 since last scrape of Spaces metrics from Cloud Foundry | |
| *metrics.namespace*_last_spaces_scrape_duration_seconds | Duration of the last scrape of Spaces metrics from Cloud Foundry | |

## Acknowledgements

Thanks to [Michal Kuratczyk][mkuratczyk] who has also been working on a [cccf_exporter][cccf_exporter].

## Contributing

Refer to the [contributing guidelines][contributing].

## License

Apache License 2.0, see [LICENSE][license].

[binaries]: https://github.com/cloudfoundry-community/cf_exporter/releases
[cccf_exporter]: https://github.com/mkuratczyk/cfcc_exporter
[cloudfoundry]: https://www.cloudfoundry.org/
[contributing]: https://github.com/cloudfoundry-community/cf_exporter/blob/master/CONTRIBUTING.md
[faq]: https://github.com/cloudfoundry-community/cf_exporter/blob/master/FAQ.md
[golang]: https://golang.org/
[license]: https://github.com/cloudfoundry-community/cf_exporter/blob/master/LICENSE
[manifest]: https://github.com/cloudfoundry-community/cf_exporter/blob/master/manifest.yml
[mkuratczyk]: https://github.com/mkuratczyk
[prometheus]: https://prometheus.io/
[prometheus-boshrelease]: https://github.com/cloudfoundry-community/prometheus-boshrelease
