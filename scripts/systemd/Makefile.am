# Network UPS Tools: scripts/systemd

EXTRA_DIST = README.adoc

if HAVE_SYSTEMD

systemdsystemunit_DATA = \
        nut-driver-enumerator.service \
        nut-driver-enumerator.path \
        nut-driver@.service \
        nut-monitor.service \
        nut-server.service  \
        nut-driver.target   \
        nut.target

systemdtmpfiles_DATA = \
        nut-common-tmpfiles.conf

EXTRA_DIST += nut-driver.target nut.target

systemdshutdown_SCRIPTS = nutshutdown

libexec_SCRIPTS = ../upsdrvsvcctl/nut-driver-enumerator.sh

sbin_SCRIPTS = ../upsdrvsvcctl/upsdrvsvcctl

else
EXTRA_DIST += \
	nut-driver@.service.in nut-monitor.service.in \
	nut-server.service.in nutshutdown.in nut-driver.target nut.target \
	nut-driver-enumerator.path.in nut-driver-enumerator.service.in

# NOTE: Do not EXTRA_DIST nut-common-tmpfiles.conf.in - it is generated per build
endif

SPELLCHECK_SRC = README.adoc

# NOTE: Due to portability, we do not use a GNU percent-wildcard extension:
#%-spellchecked: % Makefile.am $(top_srcdir)/docs/Makefile.am $(abs_srcdir)/$(NUT_SPELL_DICT)
#	$(MAKE) -s -f $(top_builddir)/docs/Makefile SPELLCHECK_SRC_ONE="$<" SPELLCHECK_SRCDIR="$(srcdir)" SPELLCHECK_BUILDDIR="$(builddir)" $@

# NOTE: Portable suffix rules do not allow prerequisites, so we shim them here
# by a wildcard target in case the make implementation can put the two together.
*-spellchecked: Makefile.am $(top_srcdir)/docs/Makefile.am $(abs_srcdir)/$(NUT_SPELL_DICT)

.sample.sample-spellchecked:
	$(MAKE) -s -f $(top_builddir)/docs/Makefile SPELLCHECK_SRC_ONE="$<" SPELLCHECK_SRCDIR="$(srcdir)" SPELLCHECK_BUILDDIR="$(builddir)" $@

.in.in-spellchecked:
	$(MAKE) -s -f $(top_builddir)/docs/Makefile SPELLCHECK_SRC_ONE="$<" SPELLCHECK_SRCDIR="$(srcdir)" SPELLCHECK_BUILDDIR="$(builddir)" $@

spellcheck spellcheck-interactive spellcheck-sortdict:
	$(MAKE) -f $(top_builddir)/docs/Makefile SPELLCHECK_SRC="$(SPELLCHECK_SRC)" SPELLCHECK_SRCDIR="$(srcdir)" SPELLCHECK_BUILDDIR="$(builddir)" $@

CLEANFILES = *-spellchecked

MAINTAINERCLEANFILES = Makefile.in .dirstamp

# Generated by autogen.sh and needed to run the configure script:
MAINTAINERCLEANFILES += nut-common-tmpfiles.conf.in
