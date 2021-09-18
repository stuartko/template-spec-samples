## Authoring and Contributing Built-in Template Specs

This documents provides general information on what built-in template specs are, and the process involved to contribute new built-in template specs for consumption by a wider population.

### What are built-ins?
Built-in template specs are [template specs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-specs?tabs=azure-powershell) that deploy cloud components/settings that fulfill scenarios that are seen as useful for a wide variety of customers across Azure. Unlike private template specs which are only available to customers (tenants) who created them, built-in template specs are available to all customers in a specific cloud (such as the Public cloud, or the Chinese national cloud, etc. etc.). Essentially they are "global" template specs that any customer can deploy from any region, and they'll behave in the same way for each customer.

They share all the same schemas and properties as customer created template specs (including versions), except built-ins are read-only resources that are accessible to anyone (there is no need to manage access rights to built-in template specs).

Examples of useful built-ins include those that apply certain standards/policies (such as ISO 27001) to existing resources, or built-ins that simplify common deployment scenarios (like deploying a Windows VM).

### How do I contribute a new built-in?

Before continuing it's important to determine whether or not the scenario the underlying Azure Resource Manager template fulfills meets the guidelines for being a built-in template spec. Ask yourself:

 - Is it a scenario that will be commonly used by many customers across Azure without requiring tweaks to the template itself?
 - Is it a scenario that works well "out of the box" (i.e. without a very specific complex environment already setup)?

If the answer to both of these questions is yes, you're on your way towards contributing a built-in. For a new built-in contribution you can follow these steps:

#### Step 1. Author the template spec in your own subscription

Before submitting a built-in, you should create a private template spec that mirrors what you'd like to submit as a built-in. The purpose is to allow you to test the template spec in your own environment before exporting it for use as a built-in. If the template spec has parameters, make sure they have helpful descriptions before continuing to the next step.

#### Step 2: Export the template spec to a local directory

#### Step 3. Create a fork of the public template spec repo

If you're not a Microsoft employee, you should fork the [public template specs repo](https://github.com/Azure/template-specs/tree/master) (For more info on how to fork a repo see '[Fork a repo - GitHub Docs](https://docs.github.com/en/get-started/quickstart/fork-a-repo)').

If your a Microsoft employee with Azure source permissions you can simply create a new branch of the repo in github.
