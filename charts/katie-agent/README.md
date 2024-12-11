# Katie-Agent Helm Chart

__TBD__ This README.md needs to be completed.

## Installing

### Mandatory Values

There are some mandatory values which must be supplied.  The following example `values.yaml` file shows these, with placeholders.  Fill in your own details as required prior to installing the chart.

```yaml
config:
  endpoint:
    apiKey: YOUR_API_KEY
  cluster:
    name: "Your Cluster Name"
```

The key `config.cluster.name` is defaulted to `Default Cluster` - if this isn't okay for you (perhaps beacuse you have multiple clusters, or which to have a more descriptive cluster name), it can be changed.

#### API Key Alternatives

The destination for the `config` element is a `ConfigMap`.  If you wish to store the API key somewhere else, omit this element from the values file, and supply a block in `env` conformant with `Pod > .spec.containers.env` which will be inserted varbatim into the deployment.  

This block could, for example, use `valueFrom` together with `secretKeyRef` to obtain the `apiKey` from a secret.

### Application Privileges and RBAC

If `serviceAccount.create` is `true` (default), the chart will create a Service Account for the agent.

In this case, two Cluster Roles will be created:  one with read-write privileges and one with read-only.

The read-write version is default but the read-only version can be selected by setting `config.cluster.role.readOnly` to `false`.

The difference is in the verbs allowed against the cluster.  The read-only version allows only:
* GET
* LIST
* WATCH

... while the read-write version adds:
* CREATE
* DELETE
* DELETECOLLECTION
* PATCH
* UPDATE

If you wish to create your own RBAC constellation, set `serviceAccount.create` to `false` and ensure a service account exists prior to deploying.  The name of this account is of the form `RELEASE_NAME-katie-agent`.  So, for example, if your release name was 'production', the name sought for the `serviceAccount` would be `production-katie-agent`.

### Examples

__TBD__
