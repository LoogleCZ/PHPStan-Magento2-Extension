# PHPStan extension for Magento 2

This repository contains set of rule and exclusions for PHPStan in order to be able to get best of the PHPStan static analysis with respect to some nasty things Magento does. 

## Exclusion of errors

- Missing type in interceptor method
	- Since you need to copy part of the original method's signature, you are sometimes forced to use not-well typed arguments. This extension will ignore such errors.

## Stubs

Various stubs for different classes that are vaguely typed or there is error in the type hint.

## Collection templates

Magneto 2 collections offers you a way how to manipulate with objects in bulk. However, PHPStan cannot interfere specific type of item from the collection itself.
In this extension, there are stubs for the Collection classes that allows you to have properly typed collection items that can help you
with static analysis. 

Stubs are available for following classes:

- `\Magento\Framework\Model\ResourceModel\Db\Collection\AbstractCollection`
- `\Magento\Framework\Data\Collection\AbstractDb`
- `\Magento\Framework\Data\Collection`

### Usage

All you need to do is include `@extends AbstractCollection<\Vendor\Module\Model\Element>` in class-level PHPDoc. For example: 

```php
<?php

declare(strict_types=1);

namespace Vendor\Module\Model\ResourceModel\Element;

use Magento\Framework\Model\ResourceModel\Db\Collection\AbstractCollection;

/**
 * @extends AbstractCollection<\Vendor\Module\Model\Element>
 */
class Collection extends AbstractCollection
{
    protected function _construct()
    {
        $this->_init(
            \Vendor\Module\Model\Element::class,
            \Vendor\Module\Model\ResourceModel\Element::class
        );
    }
}
```

If you do not work with DB collection, you will use similar annotation for other collection classes.
