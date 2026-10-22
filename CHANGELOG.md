Mugo Content Class Manager changelog
====================================

The changes of each release, newest first. Earlier releases are described by their tags
(https://github.com/se7enxweb/mugocontentclassmanager/tags).

1.1.1 (2026-10-21)
------------------

- Updated: The Objects by content class tab of the top menu shows the diagram-2 icon in the
  admin4 design (`Icon=diagram-2` in [Topmenu_contentclassmanager] of menu.ini.append.php).
  Older admin designs ignore the setting.
- Updated: The package is published as se7enxweb/mugocontentclassmanager. composer.json requires
  PHP 8.0 and the Exponential legacy installer, states the license as GPL-2.0-only, links the
  issues and the source, and lists Mugo Web and 7x as maintainer.
- Updated: ezinfo.php and extension.xml state the release (they said 1.0 since 2012), the
  copyright, the license and the website.
- Added: The text of the GNU GPL v2 as LICENSE.
- Updated: The README is rewritten for new users: installation with Composer and by hand,
  settings, usage with example addresses, permissions, known limits and troubleshooting.
  doc/README is folded into it and removed.
- Added: This changelog.

