#
# Copyright (C) 2003-2018 Sébastien Helleu <flashcode@flashtux.org>
#
# This file is part of WeeChat, the extensible chat client.
#
# WeeChat is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
#
# WeeChat is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with WeeChat.  If not, see <http://www.gnu.org/licenses/>.
#

docdir = $(datadir)/doc/$(PACKAGE)

EXTRA_DIST = CMakeLists.txt \
             docinfo.html \
             weechat.1.cs.adoc \
             cmdline_options.cs.adoc \
             weechat_quickstart.cs.adoc \
             $(wildcard autogen/user/*.adoc) \
             $(wildcard autogen/plugin_api/*.adoc)

if MAN
  man_targets = weechat.1
  man_install = install-man
  man_uninstall = uninstall-man
endif
if DOC
  doc_targets = weechat_quickstart.cs.html
  doc_install = install-doc
  doc_uninstall = uninstall-doc
endif
all-local: $(man_targets) $(doc_targets)

# man page
weechat.1: weechat.1.cs.adoc cmdline_options.cs.adoc
	$(ASCIIDOCTOR) -a revision="WeeChat $(VERSION)" -b manpage -o weechat.1 $(abs_top_srcdir)/doc/cs/weechat.1.cs.adoc

# quickstart
weechat_quickstart.cs.html: weechat_quickstart.cs.adoc $(abs_top_srcdir)/doc/docinfo.html
	$(ASCIIDOCTOR) -a revision="$(VERSION)" -a sectanchors -a source-highlighter=prettify -o weechat_quickstart.cs.html $(abs_top_srcdir)/doc/cs/weechat_quickstart.cs.adoc

# install man/docs

install-data-hook: $(man_install) $(doc_install)

install-man:
	$(mkinstalldirs) $(DESTDIR)$(mandir)/cs/man1/
	$(INSTALL_DATA) *.1 $(DESTDIR)$(mandir)/cs/man1/

install-doc:
	$(mkinstalldirs) $(DESTDIR)$(docdir)/
	$(INSTALL_DATA) *.html $(DESTDIR)$(docdir)/

# uninstall man/docs

uninstall-hook: $(man_uninstall) $(doc_uninstall)

uninstall-man:
	$(RM) $(DESTDIR)$(mandir)/cs/man1/weechat.1
	-rmdir $(DESTDIR)$(mandir)/cs/man1

uninstall-doc:
	$(RM) $(DESTDIR)$(docdir)/*.cs.html
	-rmdir $(DESTDIR)$(docdir)

# clean

clean-local:
	-rm -f weechat.1 weechat_*.html
