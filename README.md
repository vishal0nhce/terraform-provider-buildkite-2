# Buildkite Terraform Provider

This is the official Terraform provider for [Buildkite](https://buildkite.com). The provider is listed in the [Terraform Registry](https://registry.terraform.io/) and supports terraform >= 0.13.

The provider allows you to manage resources in your Buildkite organization.

Two configuration values are required:

* An API token, generated at https://buildkite.com/user/api-access-tokens. The
  token must have the `write_pipelines` REST API scope and be enabled for GraphQL
* A Buildkite organization slug, available by signing into buildkite.com and
  examining the URL: https://buildkite.com/<org-slug>

## Documentation

The reference documentation on [the terraform registry](https://registry.terraform.io/providers/buildkite/buildkite/latest/docs)
is the recommended location for guidance on using this provider.

## Installation

To use the provider, add the following terraform:

```hcl
terraform {
  required_providers {
    buildkite = {
      source = "buildkite/buildkite"
      version = "0.0.17"
    }
  }
}

provider "buildkite" {
  # Configuration options
  api_token = "token" # can also be set from env: BUILDKITE_API_TOKEN
  organization = "slug" # can also be set from env: BUILDKITE_ORGANIZATION
}
```

## Thanks :heart:

A massive thanks to [Jarryd Tilbrook](https://github.com/jradtilbrook) for authoring the original Buildkite Terraform provider.

## License

Buildkite Terraform Provider is licensed under the MIT license.

## Local development

Contributions are welcome.

If you wish to work on the provider, you'll first need Go installed on your machine (version 1.14+ is required). Dependencies are managed via gomodules and installed automatically as required.

To compile the provider:

    make build

To run local tests that don't require any network access:

    make test

Buildkite has two APIs: REST and GraphQL. New resources should use the GraphQL API where possible, but can fallback to the REST API for resouces or properties not yet supported by GraphQL.

## Release Process

Pushing a new version tag to GitHub (or creating a new release on github.com)
will trigger a new build in the release pipeline. That pipeline will compile
the appropriate binaries, sign them, and attach them to a release in
https://github.com/buildkite/terraform-provider-buildkite.

The [terraform registry](https://registry.terraform.io) will detect the new
release on GitHub and update their own listings.
