// $id$

OVERVIEW
Multisite_search is a module which is useful for searching data from multisites.
Currently this module has limitation that it search from only one database.

DEPENDENCIES
This module depends on the search module.


INSTALLATION
If you want to visible in all sites for centrally configuration then 
Copy multisite_search folder and paste in ../sites/all/modules folder.
So that it can also configured from other site's admin.

And if only you want to visible in one site then paste there.
so that only that site's admin configured.

For installing multisite_search module first you have to enable search module.
Then enable multisite_search module.

For configuration 
GO TO Administer->Multisite Configuration 

If you dont have a prefix for your site then in textbox make a one space and enter your site URL. 
After completion you have to run cron.
