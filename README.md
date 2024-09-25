Will follow https://developer.adobe.com/commerce/php/development/components/add-admin-grid/

##
file : 'app/code/LandingPage/Form/etc/module.xml'

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="LandingPage_Form" setup_version="1.0.0"/>
</config>
```

file: 'app/code/LandingPage/Form/registration.php'

```xml
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    
     // The name of the module we're registering
    'LandingPage_Form',
    __DIR__
);
```

file 'app/code/LandingPage/Form/etc/adminhtml/routes.xml'

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
  <router id="admin">
    <route id="landingpage" frontName="landingpage">
      <module name="LandingPage_Form" before="Magento_Backend" />
    </route>
  </router>
</config>
```

file 'app/code/LandingPage/Form/etc/adminhtml/menu.xml'

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Backend:etc/menu.xsd">
  <menu>
    <add id="LandingPage_Form::home" title="Category Listing" module="LandingPage_Form" sortOrder="1000" parent="Magento_Catalog::catalog_categories" resource="Magento_Catalog::categories" action="landingpage_form/index/index" />
  </menu>
</config>
```

file: 'app/code/LandingPage/Form/etc/adminhtml/layout/landingpage_form_index_index.xml'
```xml
<?xml version="1.0" encoding="UTF-8"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
  <body>
    <referenceContainer name="content">
      <uiComponent name="landingpage_form_category_listing" />
    </referenceContainer>
  </body>
</page>
```





