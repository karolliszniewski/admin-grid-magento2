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

file : 'app/code/LandingPage/Form/view/adminhtml/ui_component/landingpage_form_category_listing.xml'

```xml
<?xml version="1.0" encoding="UTF-8"?>
<listing xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Ui:etc/ui_configuration.xsd">
  <argument name="data" xsi:type="array">
    <item name="js_config" xsi:type="array">
      <item name="provider" xsi:type="string">landingpage_form_category_listing.landingpage_form_category_listing_data_source</item>
      <item name="deps" xsi:type="string">landingpage_form_category_listing.landingpage_form_category_listing_data_source</item>
    </item>
    <item name="spinner" xsi:type="string">landingpage_form_category_columns</item>
    <item name="buttons" xsi:type="array">
      <item name="add" xsi:type="array">
        <item name="name" xsi:type="string">add</item>
        <item name="label" xsi:type="string">View Category Tree</item>
        <item name="class" xsi:type="string">primary</item>
        <item name="url" xsi:type="string">catalog/category/index</item>
      </item>
    </item>
  </argument>
  <dataSource name="landingpage_form_category_listing_data_source">
    <argument name="dataProvider" xsi:type="configurableObject">
      <argument name="class" xsi:type="string">LandingPage\Form\Ui\DataProvider\Category\ListingDataProvider</argument>
      <argument name="name" xsi:type="string">landingpage_form_category_listing_data_source</argument>
      <argument name="primaryFieldName" xsi:type="string">entity_id</argument>
      <argument name="requestFieldName" xsi:type="string">entity_id</argument>
      <argument name="data" xsi:type="array">
        <item name="config" xsi:type="array">
          <item name="update_url" xsi:type="url" path="mui/index/render" />
          <item name="storageConfig" xsi:type="array">
            <item name="indexField" xsi:type="string">entity_id</item>
          </item>
        </item>
      </argument>
    </argument>
    <argument name="data" xsi:type="array">
      <item name="js_config" xsi:type="array">
        <item name="component" xsi:type="string">Magento_Ui/js/grid/provider</item>
      </item>
    </argument>
  </dataSource>
  <listingToolbar name="listing_top">
    <bookmark name="bookmarks" />
    <columnsControls name="columns_controls" />
    <massaction name="listing_massaction">
      <argument name="data" xsi:type="array">
        <item name="data" xsi:type="array">
          <item name="selectProvider" xsi:type="string">landingpage_form_category_listing.landingpage_form_category_listing.landingpage_form_category_columns.ids</item>
          <item name="displayArea" xsi:type="string">bottom</item>
          <item name="component" xsi:type="string">Magento_Ui/js/grid/tree-massactions</item>
          <item name="indexField" xsi:type="string">entity_id</item>
        </item>
      </argument>
      <action name="delete">
        <argument name="data" xsi:type="array">
          <item name="config" xsi:type="array">
            <item name="type" xsi:type="string">delete</item>
            <item name="label" xsi:type="string" translate="true">Delete</item>
            <item name="url" xsi:type="url" path="landingpage_form/category/massDelete" />
            <item name="confirm" xsi:type="array">
              <item name="title" xsi:type="string" translate="true">Delete items</item>
              <item name="message" xsi:type="string" translate="true">Are you sure you want to delete selected items?</item>
            </item>
          </item>
        </argument>
      </action>
    </massaction>
    <filters name="listing_filters">
      <argument name="data" xsi:type="array">
        <item name="config" xsi:type="array">
          <item name="templates" xsi:type="array">
            <item name="filters" xsi:type="array">
              <item name="select" xsi:type="array">
                <item name="component" xsi:type="string">Magento_Ui/js/form/element/ui-select</item>
                <item name="template" xsi:type="string">ui/grid/filters/elements/ui-select</item>
              </item>
            </item>
          </item>
        </item>
      </argument>
    </filters>
    <paging name="listing_paging" />
  </listingToolbar>
  <columns name="landingpage_form_category_columns">
    <selectionsColumn name="ids">
      <argument name="data" xsi:type="array">
        <item name="config" xsi:type="array">
          <item name="indexField" xsi:type="string">entity_id</item>
        </item>
      </argument>
    </selectionsColumn>
    <column name="entity_id">
      <settings>
        <filter>textRange</filter>
        <label translate="true">ID</label>
        <resizeDefaultWidth>25</resizeDefaultWidth>
      </settings>
    </column>
    <column name="path">
      <settings>
        <filter>text</filter>
        <bodyTmpl>ui/grid/cells/text</bodyTmpl>
        <label translate="true">Path</label>
      </settings>
    </column>
    <column name="name">
      <settings>
        <filter>text</filter>
        <bodyTmpl>ui/grid/cells/text</bodyTmpl>
        <label translate="true">Name</label>
      </settings>
    </column>
    <column name="created_at" class="Magento\Ui\Component\Listing\Columns\Date" component="Magento_Ui/js/grid/columns/date">
      <settings>
        <filter>dateRange</filter>
        <dataType>date</dataType>
        <label translate="true">Created</label>
      </settings>
    </column>
    <actionsColumn name="actions" class="Dev\Grid\Ui\Component\Category\Listing\Column\Actions" sortOrder="200">
      <argument name="data" xsi:type="array">
        <item name="config" xsi:type="array">
          <item name="resizeEnabled" xsi:type="boolean">false</item>
          <item name="resizeDefaultWidth" xsi:type="string">107</item>
          <item name="indexField" xsi:type="string">entity_id</item>
        </item>
      </argument>
      <argument name="viewUrl" xsi:type="string">catalog/category/view</argument>
    </actionsColumn>
  </columns>
</listing>
```

file: 'app/code/LandingPage/Form/Ui/DataProvider/Category/ListingDataProvider.php'

```php
<?php
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */

namespace LandingPage\Form\Ui\DataProvider\Category;

use Magento\Framework\View\Element\UiComponent\DataProvider\DataProvider;

class ListingDataProvider extends DataProvider
{
}
```

file 'app/code/LandingPage/Form/etc/di.xml'
```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <preference for="LandingPage\Form\Api\FormDataRepositoryInterface" type="LandingPage\Form\Model\FormDataRepository" />
    <preference for="LandingPage\Form\Api\FormDataInterface" type="LandingPage\Form\Model\FormData" />
    <preference for="LandingPage\Form\Api\Data\FormDataInterface" type="LandingPage\Form\Model\FormData" />

    <type name="Magento\Framework\EntityManager\MetadataPool">
        <arguments>
            <argument name="metadata" xsi:type="array">
                <item name="LandingPage\Form\Api\Data\FormDataInterface" xsi:type="array">
                    <item name="entityTableName" xsi:type="string">landingpage_form</item>
                    <item name="identifierField" xsi:type="string">id</item>
                </item>
            </argument>
        </arguments>
    </type>

    <type name="LandingPage\Form\Controller\Index\Index"> 
        <plugin name="landingpage_redirect_based_on_route" type="LandingPage\Form\Plugin\FormRedirectPlugin" />
    </type>

        <type name="Magento\Framework\DB\Adapter\Pdo\Mysql">
        <arguments>
            <argument name="debug" xsi:type="boolean">true</argument>
        </arguments>
    </type>


    <type name="LandingPage\Form\Ui\DataProvider\Category\ListingDataProvider">
        <plugin name="landingpage_form_attributes" type="LandingPage\Form\Plugin\AddAttributesToUiDataProvider" />
    </type>

    <type name="Magento\Framework\View\Element\UiComponent\DataProvider\CollectionFactory">
        <arguments>
        <argument name="collections" xsi:type="array">
            <item name="landingpage_form_category_listing_data_source" xsi:type="string">LandingPageFormCollection</item>
        </argument>
        </arguments>
    </type>

    <virtualType name="LandingPageFormCollection" type="LandingForm\Form\Ui\DataProvider\Category\Listing\Collection">
    <arguments>
      <argument name="mainTable" xsi:type="string">catalog_category_entity</argument>
      <argument name="resourceModel" xsi:type="string">LandingPage\Form\Model\ResourceModel\Category</argument>
    </arguments>
  </virtualType>

</config>
```






