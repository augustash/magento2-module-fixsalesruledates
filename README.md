# Augustash_FixSalesRuleDates

## Overview:

This modules is a stop-gap solution to offer a fix for the issue of start/end dates being added to cart sales rule automatically. See Github [magento/magento2#6762](https://github.com/magento/magento2/issues/6122) and reference internal ticket [MAGETWO-59047](https://github.com/magento/magento2/commit/e200425c1ecec910d50660fed8c422caa8d0971b)

> In Magento 1 you could have Cart Sales Rules with no start and/or end date, i.e. codes with unlimited validity. In Magento 2, saving a rule with an empty start and/or end date will automatically fill the current date as value.
>
> ### Preconditions
>
> + Magento 2.1.x
>
> ### Steps to reproduce
>
> 1. Create new "Cart Price Rule"
> 2. Do not fill a value in "From" and "To"
> 3. Save & continue editing
>
> ### Expected result
>
> + "From" and "To" fields should be empty
> + The rule should be saved without date and be always valid
>
> ### Actual result
>
> + Todays date is filled into "From" and "To"
> + The rule is date restricted

### Proposed solution

Until such time that magento/magento2#6762 and commit #e200425c from [MAGETWO-59047](https://github.com/magento/magento2/commit/e200425c1ecec910d50660fed8c422caa8d0971b) is merged into core, we opted to override the core `\Magento\SalesRule\Controller\Adminhtml\Promo\Quote\Save` class via a `di.xml` and utilizing [`preference`](http://devdocs.magento.com/guides/v2.0/extension-dev-guide/build/di-xml-file.html#abstraction-implementation-mappings)

**TODO**

+ a [Plugin (interceptor)](http://devdocs.magento.com/guides/v2.0/extension-dev-guide/plugins.html) might be better way to tackles this to avoid modules fighting over the entire class.
