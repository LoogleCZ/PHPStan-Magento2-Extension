# PHPStan extension for Magento 2

This repository contains set of rule and exclusions for PHPStan in order to be able to get best of the PHPStan static analysis with respect to some nasty things Magento does. 

## Exclusion of errors

- Missing type in interceptor method
	Since you need to copy part of the original method's signature, you are sometimes forced to use not-well typed arguments. This extension will ignore such errors.
