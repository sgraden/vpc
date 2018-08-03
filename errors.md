---

copyright:

  years: 2018

lastupdated: "2018-07-30"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# IBM Cloud Regional Infrastructure API Service (RIAS) API error messages
{: #rias-error-messages}

When you receive an error message from the RIAS APIs, you can use the message ID to find more information about how to resolve the problem.
{:shortdesc}
		
## bad_request                                   
**Message**: The information given was invalid, malformed, or missing a required field.

To fix this problem, be sure the content of your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.
		
## bad_request_solution                         
**Message**: Please double-check the data you supplied.

To fix this problem, be sure the content of your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.
		
## client_failed_body_read                      
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## client_failed_request                         
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## client_failed_request_creation                
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## client_failed_to_get                          
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## database_failure                              
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## http_request_size_exceeded                    
**Message**: The HTTP request is too large.

This problem occurs when the payload you have sent in your request is too large. You must try again, with a smaller payload. for example, instead of trying to do everything in a single request, try creating a minimal resource in one request, and then appending state to it incrementally in several subsequent requests. Consult the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling, to see what alternatives exist.

## image_bad_file
**Message**: The image template you supplied was invalid.

Try again, providing a valid image file. Consult the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.
		
## internal_solution                             
**Message**: Please contact your administrator.

Contact your administrator.

## not_authorized                               
**Message**: The request is not authorized.

You may need to check your permissions and contact your administrator, or see the [RIAS API documentation](apis.html){: new_window}.

## not_found                                     
**Message**: Please check whether the resource you are requesting exists.

For instructions to fix this problem, see TBD
		
## over_quota                                    
**Message**: The request would exceed the quota.

The quota is given in [Getting Started](getting-started.html){: new_window}.
		
## rest_response_failed_error_unmarshal          
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## rest_response_failed_success_unmarshal      
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## rest_response_parse_failed                    
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## subnet_not_empty
**Message**: The subnet is not empty, please contact your administrator.

You may need help in deleting a subnet, or you may be trying to delete the wrong subnet. Be sure the content of your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.
		
## timeout_solution                             
**Message**: Timeout, please try again later.

Try again later. If this problem persists, contact support.
		
## validation_enum
**Message**: The value supplied was not a valid option.

To fix this problem, be sure the content of your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.

## validation_failure                            
**Message**: The JSON provided did not match the expected structure.

To fix this problem, be sure the content of your request is valid JSON and that your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.

## validation_invalid_cidr                       
**Message**: The value is not a valid CIDR.

Certain IP address ranges are reserved. More information about reserved IP ranges is available in our overview of [Using your VPC with Regions and Subnets](regions-and-subnets.html){: new_window}. For further instructions to fix this problem, you can look at TBD.

## validation_invalid_ipv4_cidr        
**Message**: The value is not a valid IPv4 CIDR.

Certain IP address ranges are reserved. More information about reserved IP ranges is available in our overview of [Using your VPC with Regions and Subnets](regions-and-subnets.html){: new_window}. For further instructions to fix this problem, see TBD.
		
## validation_invalid_ipv6_cidr
**Message**: The value is not a valid IPv6 CIDR.

For VPC Beta release, IPv6 is not supported. For further instructions to fix this problem, see TBD.

## validation_invalid_address
**Message**: The value is not a valid address.

A list of individually reserved IP addresses is given in the [About](about.html) document. More information about reserved IP ranges is available in our overview of [Using your VPC with Regions and Subnets](regions-and-subnets.html){: new_window}. For further instructions to fix this problem, see TBD.

## validation_invalid_ipv4_address
**Message**: The value is not a valid IPv4 address.

Give a valid IPv4 address. For further instructions to fix this problem, see TBD.

## validation_invalid_ipv6_address
**Message**: The value is not a valid IPv6 address.

Give a valid IPv6 address. For VPC Beta release, IPv6 is not supported. For further instructions to fix this problem, see TBD.

## validation_invalid_field_type
**Message**: The value type does not match the field type.

To fix this problem, be sure the content of your request conforms to the [RIAS API documentation](apis.html){: new_window} for the endpoint you are calling.

## validation_max_value
**Message**: The value supplied was too large.

Supply a smaller value. For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_min_value
**Message**: The value supplied was too small.

Supply a larger value. For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_not_null
**Message**: The field supplied must be null.

Be sure the value is null. For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_only_one
**Message**: The value must match one of the subschemas.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_discriminator_required
**Message**: The discriminator field requires this substructure.

If the discriminator value does not match an implicit or explicit mapping, no schema can be determined and validation SHOULD fail.

For example, if you specify
```
{
protocol: icmp
port_min: 5
port_max: 100
}
```

The protocol is `icmp`, and _port_min_ is a `tcp` field, so you'll get an error.
1. validation_discriminator_required for missing `icmp` rules
2. validation_discriminator_forbidden for `tcp` fields with `icmp` specified

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_discriminator_forbidden
**Message**: The discriminator field forbids this substructure.

For example, if you specify
```
{
protocol: icmp
port_min: 5
port_max: 100
}
```

The protocol is `icmp`, and _port_min_ is a `tcp` field, so you'll get an error.
1. validation_discriminator_required for missing `icmp` rules
2. validation_discriminator_forbidden for `tcp` fields with `icmp` specified

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_required_field
**Message**: Missing a required field.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## validation_unique_failed
**Message**: The field supplied must be unique.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## security_group_limit_exceeded
**Message**: Exceeded security group limit.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_interfaces_per_sg_exceeded
**Message**: Exceeded limit of interfaces per security group.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_sgs_per_interface_exceeded
**Message**: Exceeded limit of security groups per interface.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_rules_per_sg_exceeded
**Message**: Exceeded limit of rules per security group.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_remoting_rules_per_sg_exceeded
**Message**: Exceeded limit of remoting rules per security group.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_perm_denied
**Message**: Incorrect permissions to change the security group.

You may need to check your premissions and contact your administrator. For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_interfaces_attached
**Message**: Cannot delete the security group while interfaces are attached.

Be sure all interfaces are deleted. For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_remoting_rules
**Message**: Cannot delete the security group while remoting rules are attached.

Be sure to remove all remoting rules. For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_order_bindings
**Message**: Cannot delete the security group, it has pending orders.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_not_supported
**Message**: Security groups are not supported in the target datacenter.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_already_attached
**Message**: The interface is attached already.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_exists
**Message**: The security group already exists.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## security_group_not_attached
**Message**: The interface is not attached.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Security Groups document](security-groups.html){: new_window}.

## token_missing
**Message**: The service token was empty or did not exist in the request.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## token_invalid
**Message**: The service token was expired or invalid.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## vpc_acl_conflict                           
**Message**: Cannot delete the default network ACL, it is attached to a VPC.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Network ACLs document](using-acls.html){: new_window}.

## subnet_acl_conflict
**Message**: Cannot delete the network ACL, it is attached to a subnet.

For further instructions to fix this problem, refer to the [API documentation](apis.html) or the [Using Network ACLs document](using-acls.html){: new_window}.

## floating_ip_not_empty
**Message**: Cannot delete a server with a floating IP associated.

Be sure to disassociate the floating IP before you delete the server. For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## key_exists
**Message**: The same key content already exists.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## subject_token_missing
**Message**: Cannot generate subject token with the service token, subject token is needed.

For further instructions to fix this problem, refer to the [API documentation](apis.html){: new_window}.

## 4080000
**Message**: Timeout exceeded.

For instructions to fix this problem, see  TBD [Need a good link here, of the form shown](https://www.{DomainName}/docs/troubleshoot/ts_accessing.html#ts_err){: new_window} troubleshooting topic.

## 5000100
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## 5000101                                       
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
