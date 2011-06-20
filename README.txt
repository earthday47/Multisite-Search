OVERVIEW
Multisite Search allows you to index and search content from all sites in a Multisite configuration.
If you are looking for more powerful search integration, try the Apache Solr module:
http://drupal.org/project/apachesolr

Thanks to lebachai for permission to share with the community.
This module was initially developed for Cleveland Public Library, a website based on Drupal.

REQUIREMENTS
This modules assumes the following is true:
- You have a Multisite Drupal installation
- You are sharing tables (or know how)

MULTISITE CONCEPTS
Drupal can be configured to run multiple websites from a single code base.
To read more about multisite configuration, read the resources here: http://drupal.org/node/43816

Drupal database tables in a Multisite installation can be in separate databases, or in a single 
database using table prefixing.

SHARING MULTISITE SEARCH TABLES
It is a good idea to share the Multisite Search database tables. More information: http://drupal.org/node/22267
Edit each settings.php file and make the following edit:

Change:

$db_prefix = '';

To this:

$db_prefix = array(
  'default' => '',
  'multisite_search_dataset'  => 'shared_db.',
	'multisite_search_index'    => 'shared_db.',
	'multisite_search_sites'    => 'shared_db.',
	'multisite_search_total'    => 'shared_db.',
	'multisite_search_settings' => 'shared_db.',
);

Where 'shared_db' is the name of your shared database. You can also use table prefixing if you only have one database,
in which case you would use _ (underscore) instead of . (period);
More information: http://drupal.org/node/22267


INSTALLATION INSTRUCTIONS

1. Edit the settings.php file for all sites and share the Multisite Search tables (see above).

2. Copy the multisite_search/ files to sites/all/modules.

3. Enable Search and Multisite Search on all sites. Because of step 1, you will get database errors.

4. Visit Site configuration -> Multisite configuration or admin/settings/multisite-search/sites on
   any of the sites.

5. Add each site and its information. (See "Table Prefixing" below)

6. Re-build the search index for every site by visiting admin/settings/search on each site and 
   clicking "Re-index site".

7. Run cron for all sites.

8. If you want to replace core search, disable it at Site Building -> Themes -> Configure -> 
   Global Settings or admin/build/themes/settings/global. Then visit the Blocks page at 
   Site building -> Blocks or admin/build/block and move the "Multisite Search Block" to your 
   favorite region in your theme.


TABLE PREFIXING
The follow are some examples of how to fill out the "Table Prefix" field. It's best to use the 
database name AND the prefix whenever possible.

Example 1: One database, table prefixing

Site 1 - database.site1_
Site 2 - database.site2_
Site 3 - database.site3_

Example 2: separate databases, no prefixing

Site 1 - db1.
Site 2 - db2.
Site 3 - db3.

Example 3: mixed

Site 1 - db1.
Site 2 - db2.site2_
Site 3 - db3.site3_


CONFIGURATION SETTINGS
Once the sites are set up, visit admin/settings/multisite-search/settings to change settings.
Note: These settings only need to be changed once.

Refresh Multisite search index (in seconds):

This controls how frequently the search index is rebuilt. The default is 0 seconds, which means that the 
entire Multisite Search index will be rebuilt on every cron run (for every site). On sites with a lot of 
content, it is recommended to set this to perhaps daily (86400) or weekly (604800).

Search block label:

This is the text that is displayed on the Multisite Search block.

Search tab label:

This is the text that is displayed on the search results page tab.

Exclude unpublished nodes:

Default is to exclude. Note that core search ignores node access and only checks on node display.
This has been fixed with some SQL trickery: http://drupal.org/node/1190056
If, for some reason, you do want to search unpublished nodes, uncheck this box.

Exclude content types:

This is similar to the unpublished issue. Since Multisite Search doesn't have access to the node permissions 
in the other sites, it doesn't know what to skip. More SQL trickery has been added to work around this.