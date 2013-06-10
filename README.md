Magento Cheat Sheet
===================

Frontend `local.xml` snippets
-----------------------------

Change page template
```xml
<reference name="root">
    <action method="setTemplate"><template>page/template_file.phtml</template></action>
</reference>
```

Add/remove CSS/JS
```xml
<reference name="head">
    <action method="addItem"><type>skin_css</type><name>css/file.css</name><params/></action>
    <action method="addItem"><type>skin_js</type><name>js/file.js</name><params/></action>
    <action method="removeItem"><type>skin_css</type><name>css/file.css</name><params/></action>
    <action method="removeItem"><type>skin_js</type><name>js/file.js</name><params/></action>
</reference>
```

Move block position
```xml
<reference name="old_parent">
    <action method="unsetChild"><name>block_name</name></action>
</reference>
<reference name="new_parent">
    <action method="insert"><block>block_name</block></action>
</reference>
```

Remove block
```xml
<remove name="block_name" />
```

Add crumb to breadcrumbs
```xml
<reference name="breadcrumbs">
    <action method="addCrumb">
        <crumbName>Link Text</crumbName>
        <crumbInfo>
            <label>Link Text</label>
            <title>Link Text</title>
            <link>/link-url</link>
        </crumbInfo>
    </action>
</reference>
```

Insert CMS block - usage: `$this->getChildHtml('relevant_name')`
```xml
<block type="cms/block" name="relevant_name">
    <action method="setBlockId"><block_id>static_block_identifier</block_id></action>
</block>
```

Insert template file - usage: `$this->getChildHtml('relevant_name')`
```xml
<block type="core/template" name="relevant_name" template="page/html/template_file.phtml" />
```

Add address fields to customer signup form
```xml
<customer_account_create>
    <reference name="customer_form_register">
        <action method="setShowAddressFields"><param>true</param></action>
    </reference>
</customer_account_create>
```

Frontend template file snippets
-------------------------------

Hard coded content in templates (for translations)
```php
$text = $this->__('Content');
```

`$float_value` to currency format
```php
$amount = Mage::helper('core')->currency($float_value, true, false);
```

Get URLs
```php
$url = $this->getSkinUrl('images/file.jpg'); // Get skin asset URL
$url = Mage::helper('core/url')->getHomeUrl(); // Get home URL
$url = Mage::helper('core/url')->getCurrentUrl(); // Get current URL
$url = $this->getUrl('page.html'); // Get specific page URL
```

Get current category
```php
$_category = Mage::getModel('catalog/layer')->getCurrentCategory();
```

Load category by ID
```php
$_category = Mage::getModel('catalog/category')->load($category_id);
```

Load product by ID
```php
$_product = Mage::getModel('catalog/product')->load($product_id);
```

Load product by SKU
```php
$_product = Mage::getModel('catalog/product')->loadByAttribute('sku', $product_sku);
```

Load configurable product's children
```php
$_child_products = Mage::getModel('catalog/product_type_configurable')->getUsedProducts(null, $_product);
```

Get resized product image URL (Use in `catalog/product_view_media` blocks only)
```php
$this->helper('catalog/image')->init($_product, $_image_attribute_name)
    ->keepFrame(false) // Remove white border around images
    ->constrainOnly(true) // Don't enlarge further than original size
    ->keepAspectRatio(true) // Don't crop image
    ->resize($_image_width, $_image_height); // Resize to dimensions provided
```

Check if customer logged in
```php
$logged_in = Mage::getSingleton('customer/session')->isLoggedIn();
```

Get a clean string with no symbols or spaces
```php
$_cleaned = Mage::getModel('catalog/product_url')->formatUrlKey($_dirty);
```
