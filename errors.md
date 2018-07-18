---

copyright:

  years: 2018

lastupdated: "2018-07-18"

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
		
## `bad_request`                                   
**Message**: The information given was invalid, malformed, or missing a required field.

To fix this problem, check the content of your request conforms to the RIAS API documentation(TODO:link to RIAS API docs?) for the endpoint you are calling.
		
## `bad_request_solution`                         
**Message**: Please double-check the data you supplied.

To fix this problem, check the content of your request conforms to the RIAS API documentation(TODO:link to RIAS API docs?) for the endpoint you are calling.
		
## `client_failed_body_read`                      
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `client_failed_request`                         
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `client_failed_request_creation`                
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `client_failed_to_get`                          
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `database_failure`                              
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `http_request_size_exceeded`                    
**Message**: The HTTP request is too large.

For instructions to fix this problem, see

## `image_bad_file`
**Message**: The image template you supplied was invalid.

For instructions to fix this problem, see
		
## `internal_solution`                             
**Message**: Please contact your administrator.

Contact your administrator.

## `not_authorized`                               
**Message**: The request is not authorized.

For instructions to fix this problem, see

## `not_found`                                     
**Message**: Please check whether the resource you are requesting exists.

For instructions to fix this problem, see
		
## `over_quota`                                    
**Message**: The request would exceed the quota.
		
## `rest_response_failed_error_unmarshal`          
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `rest_response_failed_success_unmarshal`        
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `rest_response_parse_failed`                    
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `subnet_not_empty`
**Message**: The subnet is not empty, please contact your administrator.

For instructions to fix this problem, see
		
## `timeout_solution`                             
**Message**: Timeout, please try again later.

Try again later. If this problem persists, contact support.
		
## `validation_enum`
**Message**: The value supplied was not a valid option.

For instructions to fix this problem, see

## `validation_failure`                            
**Message**: The JSON provided did not match the expected structure.

For instructions to fix this problem, see

## `validation_invalid_cidr`                       
**Message**: The value is not a valid CIDR.

For instructions to fix this problem, see

## `validation_invalid_ipv4_cidr`        
**Message**: The value is not a valid IPv4 CIDR.

For instructions to fix this problem, see
		
## `validation_invalid_ipv6_cidr`
**Message**: The value is not a valid IPv6 CIDR.

For instructions to fix this problem, see

## `validation_invalid_address`
**Message**: The value is not a valid address.

For instructions to fix this problem, see

## `validation_invalid_ipv4_address`
**Message**: The value is not a valid IPv4 address.

For instructions to fix this problem, see

## `validation_invalid_ipv6_address`
**Message**: The value is not a valid IPv6 address.

For instructions to fix this problem, see

## `validation_invalid_field_type`
**Message**: The value type does not match the field type.

For instructions to fix this problem, see

## `validation_max_value`
**Message**: The value supplied was too large.

For instructions to fix this problem, see

## `validation_min_value`
**Message**: The value supplied was too small.

For instructions to fix this problem, see

## `validation_not_null`
**Message**: The field supplied must be null.

For instructions to fix this problem, see

## `validation_only_one`
**Message**: The value must match one of the subschemas.

For instructions to fix this problem, see

## `validation_discriminator_required`
**Message**: The discriminator field requires this substructure.

For instructions to fix this problem, see

## `validation_discriminator_forbidden`
**Message**: The discriminator field forbids this substructure.

For instructions to fix this problem, see

## `validation_required_field`
**Message**: Missing a required field.

For instructions to fix this problem, see

## `validation_unique_failed`
**Message**: The field supplied must be unique.

For instructions to fix this problem, see

## `security_group_limit_exceeded`
**Message**: Exceeded security group limit.

For instructions to fix this problem, see

## `security_group_interfaces_per_sg_exceeded`
**Message**: Exceeded limit of interfaces per security group.

For instructions to fix this problem, see

## `security_group_sgs_per_interface_exceeded`
**Message**: Exceeded limit of security groups per interface.

For instructions to fix this problem, see

## `security_group_rules_per_sg_exceeded`
**Message**: Exceeded limit of rules per security group.

For instructions to fix this problem, see

## `security_group_remoting_rules_per_sg_exceeded`
**Message**: Exceeded limit of remoting rules per security group.

For instructions to fix this problem, see

## `security_group_perm_denied`
**Message**: Incorrect permissions to change the security group.

For instructions to fix this problem, see

## `security_group_interfaces_attached`
**Message**: Cannot delete the security group while interfaces are attached.

For instructions to fix this problem, see

## `security_group_remoting_rules`
**Message**: Cannot delete the security group while remoting rules are attached.

For instructions to fix this problem, see

## `security_group_order_bindings`
**Message**: Cannot delete the security group, it has pending orders.

For instructions to fix this problem, see

## `security_group_not_supported`
**Message**: Security groups are not supported in the target datacenter.

For instructions to fix this problem, see

## `security_group_already_attached`
**Message**: The interface is attached already.

For instructions to fix this problem, see

## `security_group_exists`
**Message**: The security group already exists.

For instructions to fix this problem, see

## `security_group_not_attached`
**Message**: The interface is not attached.

For instructions to fix this problem, see

## `token_missing`
**Message**: The service token was empty or did not exist in the request.

For instructions to fix this problem, see

## `token_invalid`
**Message**: The service token was expired or invalid.

For instructions to fix this problem, see

## `vpc_acl_conflict`                           
**Message**: Cannot delete the default network ACL, it is attached to a VPC.

For instructions to fix this problem, see

## `subnet_acl_conflict`
**Message**: Cannot delete the network ACL, it is attached to a subnet.

For instructions to fix this problem, see

## `floating_ip_not_empty`
**Message**: Cannot delete a server with a floating IP associated.

For instructions to fix this problem, see

## `key_exists`
**Message**: The same key content already exists.

For instructions to fix this problem, see

## `subject_token_missing`
**Message**: Cannot generate subject token with the service token, subject token is needed.

For instructions to fix this problem, see

## `4080000`
**Message**: Timeout exceeded.

For instructions to fix this problem, see the [Need a good link here, of the form shown](https://www.{DomainName}/docs/troubleshoot/ts_accessing.html#ts_err){: new_window} troubleshooting topic.

## `5000100`
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
		
## `5000101`                                       
**Message**: An internal error occurred.

Try again later. If this problem persists, contact support.
