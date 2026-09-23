<!-- loiofdc78af7c69246bc87315d90a061b321 -->

# Ingest via OpenTelemetry API Endpoint

You can ship OpenTelemetry data via OpenTelemetry protocol \(OTLP\) using a combined endpoint for logs, metrics, and traces. This endpoint supports the gRPC protocol, but no other protocol formats of the OTLP specification.

> ### Note:  
> Protocols like http/protobuf or http/json can be converted to gRPC using the [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/).



<a name="loiofdc78af7c69246bc87315d90a061b321__section_t1n_q1d_dzb"/>

## Procedure

OpenTelemetry support in SAP Cloud Logging needs to be enabled with a service instance configuration parameter that can be set with service instance creation or update. Once enabled, all new service bindings and service keys contain the OTLP endpoint and credentials.

1.  Enable Endpoint via Configuration Parameter.

    OpenTelemetry ingestion must be enabled explicitly via the following in the service instance configuration:

    ```
    {
        "ingest_otlp": {
            "enabled": "true"
        }
    }
    ```

    After OpenTelemetry has been enabled, the endpoint is added to the service instance.

    > ### Note:  
    > By default, the trace pipeline assembles complete traces and populates the service map \(`otel-v1-apm-service-map index`\). If you only need raw span data and do not require service map or full trace assembly, you can enable span passthrough mode:
    > 
    > ```
    > {
    >     "ingest_otlp": {
    >         "enabled": true,
    >         "span_passthrough": true
    >     }
    > }
    > ```
    > 
   > ### Note:  
   > If you only need raw span data and do not require service map or full trace assembly, you can enable span passthrough mode (see [ingest_otlp configuration parameter](configuration-parameters-1830bca.md#loio1830bca1b060484e9cfabc0e62472e8e__table_zcy_jjx_jzb)):
   > 
   > ```
   > {
   >     "ingest_otlp": {
   >         "enabled": true,
   >         "span_passthrough": true
   >     }
   > }
   > ```

2.  Retrieve Endpoint and Certificates.

    Once OpenTelemetry ingestion is enabled, all new service bindings and service keys contain the required endpoint and credentials for mutual TLS. SAP Cloud Logging only supports mTLS for the OTLP endpoint. The service key contains the following OTLP-related properties:

    ```
    {
      "credentials": {
        "ingest-otlp-endpoint":
            "ingest-otlp-sf-<your-service-id>.<your-cluster-url>:443",
        "ingest-otlp-cert":
            "-----BEGIN CERTIFICATE-----\n
             Your client certificate in PEM format\n
             -----END CERTIFICATE-----\n",
        "ingest-otlp-key":
            "-----BEGIN PRIVATE KEY-----\n
             Your client key in PCKS #8 format\n
            -----END PRIVATE KEY-----\n",
        "server-ca":
          "-----BEGIN CERTIFICATE-----\n
           Your instance server certificate in PEM format\n
           -----END CERTIFICATE-----\n",
      }
    }
    ```

    > ### Note:  
    > TLS certificates for client authentication are issued with a validity period of 90 days by default. Rotate the service key and update the credentials in all sender configurations, otherwise, ingestion will stop.

    > ### Caution:  
    > Ensure that you consider the [SAP BTP Security Recommendation BTP-CLS-0003](https://help.sap.com/docs/btp/sap-btp-security-recommendations-c8a9bb59fe624f0981efa0eff2497d7d/sap-btp-security-recommendations?seclist-index=BTP-CLS-0003&version=Cloud).

    > ### Note:  
    > Use the *certValidityDays* to configure the validity period via a service binding parameter within the range of 1 to 180 days. For example, passing `'{"ingest":{"certValidityDays":30}}` as the configuration parameter for binding creation sets the validity to 30 days.

    > ### Note:  
    > Deleting a binding doesn't revoke the corresponding certificate. [Rotate the Ingestion Root CA Certificate](rotate-the-ingestion-root-ca-certificate-bbcb3e7.md) if the root Certification Authority \(Certification Authority\) of your service instance expires soon, or the private key of a certificate was leaked.

3.  Ship OpenTelemetry data with method of choice.

    You can use the endpoint and credentials to ship OpenTelemetry signals retrieved by one of the following instrumentation options: OpenTelemetry SDK, OpenTelemetry Agent, or OpenTelemetry Collector. See [OpenTelemetry documentation on instrumentation](https://opentelemetry.io/docs/concepts/instrumentation/) for more details.




<a name="loiofdc78af7c69246bc87315d90a061b321__section_dzb_khg_cfc"/>

## Automated OpenTelemetry Exporter Configuration for Java and node.JS Applications in the Cloud Foundry Environment

This section describes streamlined ways to instrument Java and node.JS applications harmonized with other SAP offerings. This requires service bindings to contain the OpenTelemetry credentials, which is ensured for bindings created after following the above procedure.



### OpenTelemetry Java Agent Extension for SAP BTP Observability

If you are using the OpenTelemetry Java agent you can add the [BTP observability extension](https://github.com/SAP/cf-java-logging-support/tree/main/cf-java-logging-support-opentelemetry-agent-extension) to simplify shipment configuration to Cloud Logging. Follow the link for detailed information on the configuration. The extension provide new exporters `cloud-logging` for logs, metrics, and traces. These exporters scan the application's environment variables for service bindings to Cloud Logging. They automatically configures an OTLP exporter for each binding found.

> ### Note:  
> The OpenTelemetry Java Agent Extension for SAP BTP Observability is part of the SAP Java Agent Extension delivered as part of the SAP Java buildpack. Using this extension allows integration with SAP Cloud ALM and SAP Cloud Logging in the same extension.



### OpenTelemetry exporter for SAP Cloud Logging for Node.JS

If you instrumented your node.JS application with the OpenTelemetry SDK you can add the [Cloud Logging exporter](https://github.com/SAP/opentelemetry-exporter-for-sap-cloud-logging-for-nodejs) to simplify shipment configuration to Cloud Logging. Follow the link for detailed information on the configuration. The package provides exporters for logs, metrics, and traces. It scans the application's environment variables for service bindings to Cloud Logging. For each binding a OTLP exporter is configured.

> ### Note:  
> The exporter is compatible with CAP and SAP Cloud ALM libraries.



### Using user-provided Services

The Java and node.JS instrumentations support automatic scanning for bindings to managed Cloud Logging service instances. They also support user-provided service instances, if those service instances are configured correctly. User-provided services must fulfil two criteria:

1.  The need to be tagged with label *Cloud Logging*.
2.  The need to contain the OTLP credentials from a service key.
3.  Optionally, they can contain a syslog drain url, if log shipment of messages written to stdout/stderr is still required.

The following example explains the creation of a user-provided service with valid configuration using the CloudFoundry CLI.

When connected to teh source CF space which owns the managed Cloud Logging service instance that should receive the data execute the following command:

> ### Sample Code:  
> ```
> cf service-key cls test \
> | tail -n +2 \
> | jq '.credentials' \
> > credentials.json
> ```

This creates a new service key named test and saves the credentials in the JSON file credentials.json. Now connect to the CF space, where you want to create the user-provided service. If necessary transfer the credentials.json accordingly. Create the user-provided service with the following command:

> ### Sample Code:  
> ```
> cf cups <your-service-name> -p credentials.json -t "Cloud Logging"
> ```

The `-t` option sets the correct tag and is required for the libraries to detect the service bindings. If you still need a syslog drain url, you can add it to the command via the argument `-l <your-syslog-drain-url>`. You can find the url in the service key created above.

You can now bind applications to the user-provided service. They should start sending data to Cloud Logging after they are restaged. Both instrumentations will log the configured exporters during start-up. They will also emit error messages, if the configuration was incorrect.

If you need to rotate the credentials, e.g., due to expiry of the certificates, create a new service key. Instead of creating a new user-provided service, you can update your user-provided service with the new credentials. To propagate the new credentials to the applications, they need to be restaged.



<a name="loiofdc78af7c69246bc87315d90a061b321__section_kbr_nbd_dzb"/>

## Result

You can analyze the ingested OpenTelemetry data in OpenSearch Dashboards \(see [Access and Analyze Observability Data](access-and-analyze-observability-data-dad5b01.md)\). The index names match the requirements for the default analysis features of OpenSearch Dashboards. Indices match the following patterns:

-   `logs-otel-v1-*` for logs
-   `metrics-otel-v1-*` for metrics
-   `otel-v1-apm-span-*` for traces/spans
-   `otel-v1-apm-service-map` for the service map

> ### Note:  
> Due to limitations of OpenSearch/Lucene, signal and resource attribute names have dots replaced with "@," and contain a prefix specifying the attribute type. For example, the resource attribute `service.name` is mapped to `resource.attributes.service@name`. Because of its prominent role, the service name is also available as a field `serviceName`, which reflects the open-source defaults.

