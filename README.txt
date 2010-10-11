// $id$

OVERVIEW
Multisite_search is a module which is useful for searching data from multisites.
This is the new 2.x brance of Multisite search. It is not compatible with the previous 
version of Multisite Search (database table changes).

DEPENDENCIES
This module depends on the Search module.

REQUIREMENTS
This modules assumes the following is true:
- You have a Multisite Drupal installation

INSTALLATION
1. Disable AND *UNINSTALL* any previous versions of Multisite Search.

2. Copy the multisite_search/ folder into the sites/all/modules directory.

CONFIGURATION
Let's say we have 3 sites we want to share. They are prefixed like so:
Site 1 - http://site1.com/ - 'site1_'
Site 2 - http://site2.com/ - 'site2_'
Site 3 - http://site3.com/ - 'site3_'

1. Install and enable Search and Multisite Search on all sites.

If you want Site 1 to be able to search all sites, do the following:
2. While logged into Site 1, go to Administer -> Site Configuration -> Multisite Configuration.
3. Add all the sites to the table using the form.

Note: You can configure cron to run on an interval. Access
Administer -> Site Configuration -> Multisite Configuration -> Multisite Cron Configuration
to set the "TTL" property. (thanks to -enzo-. http://drupal.org/node/886662)

You can search all sites from the generated block or from the 'All Sites' tab on the Search results page.

If you want all the sites to have Multisite Search, you must repeat steps 2-4 for each site.

ADVANCED CONFIGURATION - SHARE TABLES
Since doing the above for all sites is a major pain, you can also share the Multisite Search tables
and only need to do steps 2-4 once.

If you have shared tabled with the prefix 'shared_', you would add this to your settings.php file:
$db_prefix = array(
/* ..snip.. */
  'multisite_search_dataset' => 'shared_',
	'multisite_search_index'   => 'shared_',
	'multisite_search_sites'   => 'shared_',
	'multisite_search_total'   => 'shared_',
);

If you are sharing tables in a separate database, use . (period) instead of _ (underscore).

Note: When you enable Multisite Search on multiple sites after doing this, you will get DB errors.
BUT nothing is wrong.
