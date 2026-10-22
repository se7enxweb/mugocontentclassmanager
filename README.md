Mugo Content Class Manager for Exponential
==========================================

Mugo Content Class Manager adds an **Objects by content class** tab to the Exponential
administration. It lists every content class with the number of objects it has, and for each class
it pages through those objects, sorted the way you need.

It is for administrators and developers who need to find content by its type: on an unfamiliar
site where the content tree is hard to find your way around, on a site with many objects, or before
changing or removing a class. It replaces one-off PHP scripts and direct database queries.

Contents
--------

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Permissions](#permissions)
- [Upgrading](#upgrading)
- [Known limits](#known-limits)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Credits and history](#credits-and-history)

Features
--------

- **All classes at a glance** (`/contentclassmanager/main`): every content class with its id and
  its number of objects, sortable by name or id.
- **The objects of one class** (`/contentclassmanager/view/<class id>`): the main node of each
  object, sortable by name, node id, publication date or modification date (newest change first
  by default), 10, 25 or 50 per page.
- **A left menu** with every class, to go from one class to the next.
- **Its own admin tab**, "Objects by content class". In the admin4 design the tab shows the
  diagram-2 icon before its name.
- No database tables and no settings to make: it reads what the content model already has.

Requirements
------------

- Exponential 6.x, with an administration siteaccess
- PHP 8.0 or later

Installation
------------

### With Composer

From the root of the Exponential installation:

```bash
composer require se7enxweb/mugocontentclassmanager
```

The Exponential legacy installer places the package in `extension/mugocontentclassmanager`.

### By hand

1. Download the latest release from https://github.com/se7enxweb/mugocontentclassmanager/releases
   (or `git clone https://github.com/se7enxweb/mugocontentclassmanager.git`).
2. Copy the folder to `extension/mugocontentclassmanager`. The folder name must be
   `mugocontentclassmanager`.

### Activate it

The extension is only useful in the administration, so activate it for the admin siteaccess, in
`settings/siteaccess/<admin siteaccess>/site.ini.append.php`:

```ini
[ExtensionSettings]
ActiveAccessExtensions[]=mugocontentclassmanager
```

or for every siteaccess, in `settings/override/site.ini.append.php`:

```ini
[ExtensionSettings]
ActiveExtensions[]=mugocontentclassmanager
```

Then regenerate the autoloads and clear the caches, from the installation root:

```bash
php bin/php/ezpgenerateautoloads.php -e
php bin/php/ezcache.php --clear-all
```

Configuration
-------------

There is nothing to configure. The extension adds to these settings, which you can override:

- `menu.ini`: the tab `[Topmenu_contentclassmanager]` (its name, tooltip and icon) and the title
  of the left menu:
  ```ini
  [Leftmenu_contentclassmanager]
  Name=Classes
  ```
- `module.ini`: the module `contentclassmanager`.
- `design.ini`: its admin templates and the stylesheet `carets.css` (the sort arrows).

The number of objects per page is the user's own admin list limit (`admin_list_limit`, the same
preference the content lists use), chosen with the 10, 25 and 50 links above the list.

Usage
-----

1. Sign in to the administration and open the **Objects by content class** tab.
2. The page lists every class with its id and number of objects. Click a column heading to sort
   by it; click it again to reverse the order. The address keeps the sort, for example
   `/contentclassmanager/main/(sort_by)/id/(ascending)/false`.
3. Click a class to see its objects, for example `/contentclassmanager/view/16`. Each row links to
   the object's main node, shows its node id, visibility, publication and modification dates,
   and has an edit button.
4. Sort by name, node id, published or modified, and page through the list:
   `/contentclassmanager/view/16/(sort_by)/published/(ascending)/true/(offset)/50`.
5. Use the left menu to switch to another class.

Permissions
-----------

Every view needs the policy **contentclassmanager/view**. Administrators have it already; give it
to other roles in **User accounts → Roles and policies** to let them use the tab. The lists show
nodes through the normal content fetch, so users see only the objects they may read.

Upgrading
---------

1. Replace the extension's folder with the new release
   (`composer update se7enxweb/mugocontentclassmanager`, or copy the new files over the old ones).
2. Regenerate the autoloads and clear the caches (see [Activate it](#activate-it)).
3. Read [CHANGELOG.md](CHANGELOG.md).

Known limits
------------

- The object count of a class counts all its objects, while the list shows only objects that
  have a main node the user may read, so the two can differ (for example for objects in the
  trash, drafts never published, or content the user has no access to).
- The templates are written for the admin designs; there is no page for public siteaccesses.
- The texts use the kernel's admin translations; there are no translations of its own.

Troubleshooting
---------------

- **The tab is missing.** Check that the extension is active for the admin siteaccess, clear the
  caches, and give your role `contentclassmanager/view`.
- **The tab has no icon.** Icons are drawn by the admin4 design; older admin designs show the
  name only.
- **"Module not found" for contentclassmanager.** Regenerate the autoloads and clear the INI cache
  (`php bin/php/ezcache.php --clear-tag=ini`).

Bug reports: https://github.com/se7enxweb/mugocontentclassmanager/issues

Contributing
------------

Pull requests are welcome at https://github.com/se7enxweb/mugocontentclassmanager.

License
-------

Mugo Content Class Manager is licensed under the GNU General Public License v2.0; see
[LICENSE](LICENSE).

Credits and history
-------------------

Mugo Web (https://www.mugo.ca) wrote Mugo Content Class Manager in 2012 for eZ Publish, the
content management system that preceded Exponential, and described it in
"Viewing eZ Publish content objects by content class" on its blog. It was published as
`mugoweb/mugocontentclassmanager` (https://github.com/mugoweb/mugocontentclassmanager). Peter
Keung, Elio Sbrocchi, Kosmin and Sebastian Blank (main nodes only) contributed. 7x maintains this
fork for Exponential.

- Copyright (C) 2012 - 2018 Mugo Web
- Copyright (C) 1998 - 2026 7x
