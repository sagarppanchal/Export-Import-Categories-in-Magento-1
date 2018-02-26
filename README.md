# Export-Import-Categories-in-Magento-1
How To Export and Import Categories in Magento


Step 1 of 4: Write the following code in category.php and place it to root directory. Run this file at browser http://www.example.com/exportCategories.php. It will generate a CSV file  Categories.csv (export all categories).

Step 2 of 4: Import the categories

             create config.xml  at app\code\local\ImpCat\Catalog\etc\config.xml

             create Category.php at app\code\local\ImpCat\Catalog\Model\Convert\Adapter\Category.php

             create ImpCat_All.xml  at  app\etc\modules
              
Step 3 of 4: create dataflow advanced profile at 

            admin > system >Import/Export > Dataflow - Advanced Profile 
            
            and give the Profile Name is 'category import'
             

      //place the following code to its Actions xml box 

        <action type="dataflow/convert_adapter_io" method="load">
           <var name="type">file</var>
           <var name="path">var/import</var>
           <var name="filename"><![CDATA[Categories.csv]]></var>
           <var name="format"><![CDATA[csv]]></var>
         </action>
         <action type="dataflow/convert_parser_csv" method="parse">
           <var name="delimiter"><![CDATA[,]]></var>
           <var name="enclose"><![CDATA["]]></var>
           <var name="fieldnames">true</var>
           <var name="store"><![CDATA[0]]></var>
           <var name="number_of_records">1</var>
           <var name="decimal_separator"><![CDATA[.]]></var>
           <var name="adapter">catalog/convert_adapter_category</var>
           <var name="method">parse</var>
         </action>

Step 4:  

         Put Categories.csv into var/import/ and
         removed cat_id colums from csv.
         remove first two rows.
         remove all Default Category/ from categories colunn in Categories.csv
         
         Now to Run Profile admin > system > Import/Export > Dataflow-Advanced Profile
         run 'category import' profile  from Run Profile > click 'Run Profile in Popup'
         import of category now start and automatically created category.

