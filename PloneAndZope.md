## Resolving the `Malformed MIME type (BROKEN)` AROfficeTransforms 0.9.4 installation error ##

### [TraceBack](http://pastebin.com/f60b24b4d) ###
`Traceback (innermost last):`<br />
`  Module ZPublisher.Publish, line 119, in publish`<br />
`  Module ZPublisher.mapply, line 88, in mapply`<br />
`  Module ZPublisher.Publish, line 42, in call_object`<br />
`  Module Products.CMFQuickInstallerTool.QuickInstallerTool, line 589, in installProducts`<br />
`  Module Products.CMFQuickInstallerTool.QuickInstallerTool, line 514, in installProduct`<br />
`   - __traceback_info__: ('AROfficeTransforms',)`<br />
`  Module Products.ExternalMethod.ExternalMethod, line 231, in __call__`<br />
`   - __traceback_info__: ((<PloneSite at /Plone>,), {}, None)`<br />}}}
`  Module /Applications/Plone/buildout-cache/eggs/Products.AROfficeTransforms-0.9.4-py2.4.egg/Products/AROfficeTransforms/Extensions/Install.py, line 13, in install`<br />
`  Module Products.PortalTransforms.TransformEngine, line 391, in manage_addTransform`<br />
`  Module Products.PortalTransforms.TransformEngine, line 265, in _mapTransform`<br />
`  Module Products.MimetypesRegistry.MimeTypesRegistry, line 218, in lookup`<br />
`   - __traceback_info__: ("'BROKEN'", 'BROKEN')`<br />
`  Module Products.MimetypesRegistry.MimeTypesRegistry, line 455, in split`<br />
`MimeTypeException: Malformed MIME type (BROKEN)`<br />
### Resolution ###
  * Create a symbolic link from `/opt/local/bin/pdftohtml` to `/usr/bin/pdftohtml` - assuming that PDFtoHTML was installed there
  * Alternatively, find another way to install PDFtoHTML

## PloneSVNView and Plone (latest) on Mac OS X ##
  * Install Plone (of course!) using the handy DMG at
  * Grab [py24\_pysvn\_svn144-1.5.2-872-i386.dmg](http://pysvn.tigris.org/files/documents/1233/38910/py24_pysvn_svn144-1.5.2-872-i386.dmg), or look for another compatible version [here](http://pysvn.tigris.org/servlets/ProjectDocumentList?folderID=5841&expandFolder=5841&folderID=0) if that doesn't work
  * Grab [PloneSVNView-0.5.tar.gz](http://quest.windwards.net/quest/hacking/plonesvnview/PloneSVNView-0.5.tar.gz)

### Attempting to Install PySVN for PloneSVNView ###
  * Mount `py24_pysvn_svn144-1.5.2-872-i386.dmg` and copy `/Volumes/py24_pysvn_svn144-1.5.2-872-i386/py24_pysvn_svn144-1.5.2-872-i386.pkg/Contents/Archive.pax.gz` to `$HOME/PSVN-24/file.pax.gz`
  * Switch to `$HOME/PSVN-24` and move the `pysvn` directory to `/Applications/Plone/Python-2.4/lib/python2.4`
  * Dispose of the `$HOME/PSVN-24` directory along with it's contents
  * Unmount the `py24_pysvn_svn144-1.5.2-872-i386` volume

### Attempting to Install PloneSVNView itself ###
  * Extract the contents of `PloneSVNView-0.5.tar.gz`
  * Move the `PloneSVNView` directory to `/Applications/Plone/zinstance/products`, and dispose of the `PloneSVNView-0.5.tar.gz` archive
  * Carefully restart your Zope/Plone instance in the usual manner (by hitting the `Restart` button at the `Control_Panel` Zope Management Interface page, or hitting `Stop` and then `Start` after waiting a few moments, in the PloneController GUI application)