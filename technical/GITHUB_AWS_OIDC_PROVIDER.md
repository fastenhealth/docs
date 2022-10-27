Register Github as an OpenID OIDC identity provider for AWS
This allows us to access out AWS environment without storing IAM credentials in GitHub

This identity provider registration step is global and only needs to be done once for the account
the various roles used for deployments are defined in the app component, as each app has a different role


- https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services
- https://www.cloudquery.io/blog/keyless-access-to-aws-in-github-actions-with-oidc
- https://www.eliasbrange.dev/posts/secure-aws-deploys-from-github-actions-with-oidc/
- https://github.com/unfunco/terraform-aws-oidc-github