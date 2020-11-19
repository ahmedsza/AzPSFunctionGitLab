# Deploy Powershell Azure Function with GitLab

This is an example of taking a hello world Azure Powershell function and deploying with GitLab Pipeline

Steps

1) Create a service principal in Azure with appropriate permissions 
    az login
    # be sure to grab all the values from above, especially appid, password and tenant
    az ad sp create-for-rbac --name http://GitLabTest
    # setup permissions, could probably be more granular (i.e create rg first and then just give permissions on the rg)
    az role assignment create --assignee <<appid from above>> --role Contributor
2) create a resource group in Azure (below uses powershell)
    $rgname='AzPSFunction-rg'
    $location='westeurope'
    az group create --name $rgname --location $location
3) In Gitlab setup the appropriate variables including
    - azurefunctionappname (the unique name for your azure function)
    - location (pref same location as created in step 3)
    - rgname  (should be same as resource group created above)
    - storageaccountname  (unique storage account name)
    - SP_APP_ID (taken from step 2)
    - SP_PASSWORD (taken from step 2)
    - SP_TENANT_ID (taken from step 2)
4) Deploy the code to GitLab
