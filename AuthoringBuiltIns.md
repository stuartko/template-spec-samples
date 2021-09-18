

## Authoring and Contributing Built-in Template Specs

This documents provides general information on what built-in template specs are, and the process involved to contribute new built-in template specs for consumption by a wider population.

### What are built-ins?
Built-in template specs are [template specs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-specs?tabs=azure-powershell) that deploy cloud components/settings that fulfill scenarios that are seen as useful for a wide variety of customers across Azure. Unlike private template specs which are only available to customers (tenants) who created them, built-in template specs are available to all customers in a specific cloud (such as the Public cloud, or the Chinese national cloud, etc. etc.). Essentially they are "global" template specs that any customer can deploy from any region, and they'll behave in the same way for each customer.

They share all the same schemas and properties as customer created template specs (including versions), except built-ins are read-only resources that are accessible to anyone (there is no need to manage access rights to built-in template specs).

Examples of useful built-ins include those that apply certain standards/policies (such as ISO 27001) to existing resources, or built-ins that simplify common deployment scenarios (like deploying a Windows VM).

