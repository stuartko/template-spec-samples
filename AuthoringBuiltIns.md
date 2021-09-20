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

#### Step 1: Validate your template/template spec functionality 

Before submitting a built-in, you should create a private template spec (in your own subscription) that mirrors what you'd like to submit as a built-in. The purpose is to allow you to test the template spec in your own environment before packaging the template for built-in submission. If the template spec has parameters, make sure they have helpful descriptions before continuing to the next step.

#### Step 2. Create a fork of the public template spec repo

If you're not a Microsoft employee, you should fork the [public template specs repo](https://github.com/Azure/template-specs/tree/master) (For more info on how to fork a repo see '[Fork a repo - GitHub Docs](https://docs.github.com/en/get-started/quickstart/fork-a-repo)').

If your a Microsoft employee with Azure source permissions you can simply create a new branch of the repo in github.

#### Step 3: Add the main template/artifacts to your local enlistment

In your forked/branched repository, navigate to the built-ins/samples root directory and create a directory for your template spec version using the structure:

* /*{templateSpecId}*/versions/*{versionName}*

Keep in mind that *templateSpecId* will be the resource name customers use in the future to access your built-in template spec, and it **cannot** be changed after the template spec has been published... so be sure to choose a name that will stand the test of time.

For *versionName* you should select a version that aptly describes your initial version. For most cases, 'v1' is appropriate. However if your built-in targets a standard that is date driven, it's recommended that you include the targeted date within your version... For example for a built-in targeting targeting the 2020 version of SWIFT compliance, your version name could be "2020.v1".

After you've created the version directory. It's time to add the templates/artifacts json to the directory. If your template spec contains a template that does not leverage template spec artifacts (ie: relative paths), this process is extremely simple... Just copy your Azure Resource Manager template to:

* /*{templateSpecId}*/versions/*{versionName}*/**mainTemplate.json**

**If your template spec contains artifacts** you'll need to export the template spec using [Az Powershell](https://docs.microsoft.com/en-us/powershell/azure/new-azureps-module-az) cmdlets. That process is as follows:

* Use `Set-AzContext` to set the subscription where your template spec is located to the active context
* Run `Export-AzTemplateSpec -ResourceGroupName {rgName} -Name {templateSpecId} -Version {versionName} -OutputFolder {theRootBuiltInsDirectory}/{templateSpecId}/versions/{versionName}`
* Navigate to the output folder and rename the .json file created there (it'll be named with the format "*{templateSpecId}.{versionName}.json*") to **mainTemplate.json**

#### Step 4: Add metadata for your template spec
