#
#  Makefile --
#
#     Makefile for building icons for Wings 3D.
#
#  Copyright (c) 2001-2013 Bjorn Gustavsson
#
#  See the file "license.terms" for information on usage and redistribution
#  of this file, and for a DISCLAIMER OF ALL WARRANTIES.
#
#     $Id: Makefile,v 1.7 2006/08/23 02:56:49 antoneos Exp $
#

include ../erl.mk

.SUFFIXES: .erl .jam .beam .yrl .xrl .bin .mib .hrl .sgml .html .ps .3 .1 \
	.fig .dvi .tex .class .java .pdf .psframe .pscrop

ESRC=.
EBIN=../ebin

ICONSETS= \
	classic \
	bluecube \
	purpletube

ICONSIZE= \
	48x48 \
	256x256 \
	379x379

TARGET_FILES = $(ICONSETS:%=$(EBIN)/wings_icon_%.bundle) \
		$(ICONSIZE:%=$(EBIN)/wings_icon_%.png)

GEN_PS_ICONS=$(wildcard orig/bluecube-assests/*.png)
PS_ICONS=$(patsubst %,bluecube/%,$(notdir $(GEN_PS_ICONS)))

# ----------------------------------------------------
# FLAGS
# ----------------------------------------------------
ERL_FLAGS += -pa ../../wings/ebin
ERL_COMPILE_FLAGS += -I ../.. -Werror +debug_info

# ----------------------------------------------------
# Targets
# ----------------------------------------------------

opt debug: collect_bmp.beam $(TARGET_FILES)

bluecube/%.png: orig/bluecube-assests/%.png
	mv $? $@

$(EBIN)/wings_icon_%.bundle: %/*.bmp %/*.png collect_bmp.beam about_wings.bmp
	$(ERL) $(ERL_FLAGS) -noinput -run collect_bmp start . $(ESRC)/$* $@ -s erlang halt

clean:
	for ICONSET in $(ICONSETS); do \
		rm -f $(EBIN)/wings_icon_$$ICONSET.bundle; \
	done
	rm -f collect_bmp.beam
	@echo

$(EBIN)/%.png:
	install $*.png $@

%.beam: $(ESRC)/%.erl
	$(ERLC) $(ERL_COMPILE_FLAGS) -o. $<
