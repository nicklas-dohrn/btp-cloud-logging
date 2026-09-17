<!-- loio1830bca1b060484e9cfabc0e62472e8e -->

# Configuration Parameters

SAP Cloud Logging supports the following parameters for `create service` and `update service` operations.

> ### Note:  
> Configuration parameters may impact pricing. Pricing information is available via [Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/cloud-logging?tab=service_plan&service_plan=overall-(large,-standard,-and-dev)&region=all&commercialModel=btpea) and [SAP Cloud Logging Capacity Unit Estimator](https://sap-cloud-logging-estimator.cfapps.us10.hana.ondemand.com/).



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_gzh_zcn_lzb"/>

## Configuration Parameters


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

backend

</td>
<td valign="top">

No

</td>
<td valign="top">

[backend](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_xyd_p3x_jzb) 

</td>
<td valign="top">

Configures the OpenSearch backend.

</td>
</tr>
<tr>
<td valign="top">

dashboards

</td>
<td valign="top">

No

</td>
<td valign="top">

[dashboards](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_gqx_w3x_jzb) 

</td>
<td valign="top">

Configures the dashboards UI.

</td>
</tr>
<tr>
<td valign="top">

ingest

</td>
<td valign="top">

No

</td>
<td valign="top">

[ingest](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_brp_bjx_jzb) 

</td>
<td valign="top">

Configures the ingest endpoint.

</td>
</tr>
<tr>
<td valign="top">

ingest\_otlp

</td>
<td valign="top">

No

</td>
<td valign="top">

[ingest\_otlp](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_zcy_jjx_jzb) 

</td>
<td valign="top">

Configures the data ingestion over the ingest-otlp endpoint \(OpenTelemetry Protocol\).

</td>
</tr>
<tr>
<td valign="top">

feature\_flags

</td>
<td valign="top">

No

</td>
<td valign="top">

String Array

</td>
<td valign="top">

Used for enabling specific/experimental features specified as array:

`"feature_flags": [ "feature-1", "feature 2" ]`. Please omit or keep empty by default.

Currently, there are no available feature flags.

</td>
</tr>
<tr>
<td valign="top">

retention\_period

</td>
<td valign="top">

No

</td>
<td valign="top">

Integer

</td>
<td valign="top">

The time in days until data \(see [Ingest Observability Data](ingest-observability-data-ba16ff7.md)\) is deleted. The range is between `1` and `90` and it defaults to `7`. Data can also be deleted if the file grows too large, due to size-based curation. Changing this parameter will only affect newly-created indices.

</td>
</tr>
<tr>
<td valign="top">

oidc

</td>
<td valign="top">

No

</td>
<td valign="top">

[oicd](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_nxs_3wl_53c)

</td>
<td valign="top">

Configures the OIDC Integration to authenticate in dashboards.

</td>
</tr>
<tr>
<td valign="top">

saml

</td>
<td valign="top">

No

</td>
<td valign="top">

[saml](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_nrv_sjx_jzb) 

</td>
<td valign="top">

Configures the SAML Integration to authenticate in dashboards.

</td>
</tr>
<tr>
<td valign="top">

rotate\_root\_ca

</td>
<td valign="top">

No

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

> ### Note:  
> Updating this parameter can invalidate bindings permanently

Controls the rotation of the ingestion root Certificate Authority \(CA\) certificate. Defaults to `false`.

Refer to [Rotate the Ingestion Root CA Certificate](rotate-the-ingestion-root-ca-certificate-bbcb3e7.md) for more details.

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_fhr_wcn_lzb"/>

## Configuration Parameters for `backend`


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

max\_data\_nodes

</td>
<td valign="top">

No

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Indirectly, this parameter sets the maximum disk size for storing observability data as described in [Service Plans](service-plans-a9d2d1b.md). This parameter has no effect for the *dev* plan. Needs to be between `2` and `10`. The default is `10`.

</td>
</tr>
<tr>
<td valign="top">

min\_data\_nodes

</td>
<td valign="top">

No

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Specifies the minimum number of OpenSearch data nodes to remain provisioned, regardless of auto-scaling. This allows for prescaling the minimum disk size for storing observability data as described in [Service Plans](service-plans-a9d2d1b.md). Maintaining a minimum baseline of data nodes can help mitigate potential ingestion bottlenecks. This parameter has no effect for the `dev` plan. Needs to be between `2` and `10`, and less than or equals to `max_data_nodes`. The default is `2`.

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_hnn_zbn_lzb"/>

## Configuration Parameters for `dashboards`


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

custom\_label

</td>
<td valign="top">

No

</td>
<td valign="top">

String

</td>
<td valign="top">

Set a custom label to be displayed in OpenSearch Dashboards in the top bar to identify and distinguish multiple service instances. The label is embedded into a fixed sized element due to technical limitations. It gets cut off if the content is too long. 12 characters is ideal, and the maximum length is 20. Supported characters are `A-Z`, `a-z`, `0-9`, `#`, `+`, `-`, `_`, `/`, `*`, `(`, `)`, and space.

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_o51_4bn_lzb"/>

## Configuration Parameters for `ingest`


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

enabled

</td>
<td valign="top">

No

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Enables ingestion over the `ingest-` and `ingest-mtls-` endpoint. This includes log and metric ingestion from Cloud Foundry. Defaults to `true`.

</td>
</tr>
<tr>
<td valign="top">

max\_instances

</td>
<td valign="top">

No

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Specifies the maximum number of provisionable ingest instances, which are scaled automatically based on their overall CPU and memory utilization. Must be between `2` and `10`. Defaults to `2`. This parameter impacts peak throughput and buffering. Scale-out happens when the overall CPU utilization exceeds 80%. Scale-in happens when the overall CPU utilization or configuration parameter decreases. This parameter has no effect on the *dev* plan, which is limited to a single instance.

</td>
</tr>
<tr>
<td valign="top">

min\_instances

</td>
<td valign="top">

No

</td>
<td valign="top">

Integer

</td>
<td valign="top">

Specifies the minimum number ingest instances which are always provisioned regardless of auto-scaling. Utilized to guarantee a minimum number of running instances, support predictable workloads, and mitigate autoscaling lag during sudden ingestion bursts. Must be between `2` and `10` and less than or equals to `max_instances`. Default is `2`. This parameter has no effect on the *dev* plan, which is limited to a single instance. If `max_instances` is smaller than `min_instances`, both parameters will be set to the value of `max_instances` \(= no autoscaling\).

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_vc3_w1n_lzb"/>

## Configuration Parameters for `ingest_otlp`


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

enabled

</td>
<td valign="top">

No

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Enables ingestion over the OpenTelemetry Protocol. Defaults to `false`. For more information, see [Ingest via OpenTelemetry API Endpoint](ingest-via-opentelemetry-api-endpoint-fdc78af.md).

</td>
</tr>
<tr>
<td valign="top">

span\_passthrough

</td>
<td valign="top">

No

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

When set to `true`, spans are written to OpenSearch individually as they arrive, without assembling complete traces. Defaults to `false`.

This can be useful if you know that root/parent spans will be missing from your telemetry \(e.g., when only a subset of services in a request path emit spans\), so trace assembly cannot succeed anyway. In this case it lowers ingestion latency at the cost of trace completeness.

> ### Note:  
> When `span_passthrough` is enabled, the `otel-v1-apm-service-map` index is not populated, so the Service Map view in the Observability plugin of OpenSearch Dashboards will not function and the Trace Analytics view may show orphaned spans rather than complete trace trees.



</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_fs5_2wl_53c"/>

## Configuration Parameters for `oidc`

Configuration options for OIDC Integration. For more information, see [OIDC Integration](integrate-sap-cloud-identity-services-identity-authentication-openid-connect-with-sap-clo-b2fffa4.md).


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

enabled

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Set to `true` to enable OpenID Connect authentication.

</td>
</tr>
<tr>
<td valign="top">

admin\_group

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The OpenID group that you want to grant administrative access to. It will have permissions to modify the security module. Required if `enabled` is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

roles\_key

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The key in the JSON payload that stores the user's roles. The value of this key must be a comma-separated list of roles. For example: `groups` or `roles`. Required if `enabled` is set to `true`.

[OpenSearch docs: Configure OpenID Connect integration](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
<tr>
<td valign="top">

subject\_key

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The key in the JSON payload that stores the user's name. For example: `email` or `last_name`. Required if `enabled` is set to `true`.

[OpenSearch docs: Configure OpenID Connect integration](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
<tr>
<td valign="top">

openid\_connect\_url

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The URL of your IdP where the security plugin can find the OpenID Connect metadata/configuration settings. The URL must end with `/.well-known/openid-configuration`. Required if `enabled` is set to `true`.

[OpenSearch docs: OpenID Connect URL](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
<tr>
<td valign="top">

openid\_client\_id

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The ID of the OpenID Connect client configured in your IdP. Required if `enabled` is set to `true`.

[OpenSearch docs: OpenID Connect Configuration](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
<tr>
<td valign="top">

openid\_client\_secret

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The client secret of the OpenID Connect client configured in your IdP. Required if `enabled` is set to `true`.

[OpenSearch docs: OpenID Connect Configuration](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
<tr>
<td valign="top">

openid\_scopes

</td>
<td valign="top">

Required

</td>
<td valign="top">

String

</td>
<td valign="top">

The scope of the identity token issued by the IdP. Space-separated string list if more than one. For example: `"openid"`. Required if `enabled` is set to `true`.

[OpenSearch docs: OpenID Connect Configuration](https://opensearch.org/docs/latest/security/authentication-backends/openid-connect/)

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_m4y_p1n_lzb"/>

## Configuration Parameters for `saml`

> ### Caution:  
> Ensure that you consider the [SAP BTP Security Recommendation BTP-CLS-0001](https://help.sap.com/docs/btp/sap-btp-security-recommendations-c8a9bb59fe624f0981efa0eff2497d7d/sap-btp-security-recommendations?seclist-index=BTP-CLS-0001&version=Cloud).

Configuration to integrate the service with a SAML Idenditiy Provider \(IdP\), like SAP Cloud Identity Services - Identity Authentication \(Identity Authentication\). See [Prerequisites](prerequisites-41d8559.md) on how to integrate SAP Cloud Logging with Identity Authentication. This configuration exposes a subset of the SAML parameters of OpenSearch. Learn more about configuration parameters from [OpenSearch](https://opensearch.org/)


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Required

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

enabled

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Enables SAML authentication. We strongly recommend SAML authentication for production use cases, because of improved security and login flow. Basic authentication is configured if this parameter is set to `false`.

</td>
</tr>
<tr>
<td valign="top">

admin\_group

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

String

</td>
<td valign="top">

The SAML group to grant administrative access and permissions to modify the security module. Required if `enabled` is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

initiated

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

Boolean

</td>
<td valign="top">

Enables IdP-initiated SSO. Required if *enabled* is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

roles\_key

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

String

</td>
<td valign="top">

The list of backend\_roles will be read from this attribute during user login.

This field must be set to the corresponding attribute for IdP groups,usually `groups`. Required if *enabled* is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

idp.metadata\_url

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

URL

</td>
<td valign="top">

The URL to get the SAML IdP metadata from. Required if *enabled* is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

idp.entity\_id

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

String

</td>
<td valign="top">

The Entity ID of the SAML IdP.

Open the metadata URL in your browser and copy the full value of the `entityID` field. It is located in the first line of the response. Required if *enabled* is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

sp.entity\_id

</td>
<td valign="top">

Conditionally

</td>
<td valign="top">

String

</td>
<td valign="top">

The Entity ID of the service provider. Generally, this parameter is set to the name of your application configured in your IdP. Required if *enabled* is set to `true`.

</td>
</tr>
<tr>
<td valign="top">

sp.signature\_private\_key

</td>
<td valign="top">

No

</td>
<td valign="top">

String

</td>
<td valign="top">

The private key is used to sign the requests. This parameter must be valid base64 encoded and PKCS8 format.

</td>
</tr>
<tr>
<td valign="top">

sp.signature\_private\_key\_password

</td>
<td valign="top">

No

</td>
<td valign="top">

String

</td>
<td valign="top">

The password of the signing key, if it is encrypted.

</td>
</tr>
</table>



<a name="loio1830bca1b060484e9cfabc0e62472e8e__section_rgc_gm1_cgc"/>

## Sample Configuration Parameters in JSON

The following snippet shows a sample payload that could be used for a `standard` or `large` plan:

> ### Sample Code:  
> ```
> {
>   "backend": {
>     "max_data_nodes": 10
>   },
>   "dashboards": {
>     "custom_label": "My-Label"
>   },
>   "feature_flags": [],
>   "ingest": {
>     "enabled": true,
>     "max_instances": 10,
>     "min_instances": 3
>   },
>   "ingest_otlp": {
>     "enabled": true,
>     "span_passthrough": false
>   },
>   "retention_period": 14
> }
> ```

