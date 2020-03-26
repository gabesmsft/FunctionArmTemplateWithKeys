This is a starter sample for using ARM template to create/update Azure Functions Host keys and Function keys.<br><br>
If you do decide to create a Function key, you will need to ensure that the Function exists before you create the key, otherwise the template deployment will fail due to the Function not being found.<br><br>
Also, I made the Function key section deploy after the Host key section via dependsOn, to avoid potential conflicts with creating two keys at the same time on the same Function App.<br><br>
Functions host & function keys are each multi-level child ARM resources.<br><br>
The format of an ARM URI when there are multiple child resource levels is:<br>
ResourceProvider/parenttype/parentname/childtype1/childname1/childtypeN/childnameN<br><br>
Thus you would do the following to define the resource in the ARM template:<br>
"name": "parentname/childname1/childnameN"<br>
"type": "ResourceProvider/parenttype/childtype1/childtypeN"<br>
<br><br>
For example, the URI format for a host key is:<br> /subscriptions/sub/resourceGroups/functionsrg/providers/Microsoft.Web/sites/AppName/host/default/functionKeys/hostkey1
<br><br>
So you would have:<br>
"name": "AppName/default/hostkey1",<br>
"type": "Microsoft.Web/sites/host/functionkeys"

And the URI format for a function key is:<br> /subscriptions/sub/resourceGroups/functionsrg/providers/Microsoft.Web/sites/AppName/functions/FunctionName/keys/funkey1<br><br>
So you would have:<br>
"name": "AppName/FunctionName/funkey1",<br>
"type": "Microsoft.Web/sites/functions/keys"

 




