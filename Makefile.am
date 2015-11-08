###############################################################################
## Makefile for Northern Saami--Inari Saami
###############################################################################

VERSION=0.1.0
LANG1=sme
LANG2=smn
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =			\
	$(PREFIX1).automorf.hfst	\
	$(PREFIX1).automorf-untrimmed.hfst \
	$(PREFIX1).mor.rlx.bin		\
	$(PREFIX1).syn.rlx.bin		\
	$(PREFIX1).autobil.bin		\
	$(PREFIX1).autolex.bin		\
	$(PREFIX1).autogen.hfst		\
	$(PREFIX1).t1x.bin		\
	$(PREFIX1).t2x.bin		\
	$(PREFIX1).t3x.bin		\
	$(PREFIX2).automorf.hfst	\
	$(PREFIX2).automorf-untrimmed.hfst \
	$(PREFIX2).mor.rlx.bin		\
	$(PREFIX2).syn.rlx.bin		\
	$(PREFIX2).autobil.bin		\
	$(PREFIX2).autolex.bin		\
	$(PREFIX2).autogen.hfst		\
	$(PREFIX2).t1x.bin		\
	$(PREFIX2).t2x.bin		\
	$(PREFIX2).t3x.bin


# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Northern Saami analysis:
# -------------------

.deps/$(LANG1).automorf.hfst: $(AP_SRC1)/$(BASENAME).$(PREFIX1).LR.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

.deps/$(PREFIX1).automorf-trimmed.hfst: .deps/$(LANG1).automorf.hfst .deps/$(PREFIX1).autobil.prefixes
	hfst-compose-intersect -1 $< -2 .deps/$(PREFIX1).autobil.prefixes -o $@

$(PREFIX1).automorf.hfst: .deps/$(PREFIX1).automorf-trimmed.hfst
	hfst-fst2fst -w -i $< -o $@

$(PREFIX1).automorf-untrimmed.hfst: .deps/$(LANG1).automorf.hfst
	hfst-fst2fst -w -i $< -o $@

# -------------------
# Northern Saami generation:
# ---------------------

.deps/$(LANG1).autogen.hfst: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).RL.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

$(PREFIX2).autogen.hfst: .deps/$(LANG1).autogen.hfst
	hfst-fst2fst -O -i $< -o $@


# -------------------
# Inari Saami analysis:
# -------------------

.deps/$(LANG2).automorf.hfst: $(AP_SRC2)/$(BASENAME).$(PREFIX2).LR.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

.deps/$(PREFIX2).automorf-trimmed.hfst: .deps/$(LANG2).automorf.hfst .deps/$(PREFIX2).autobil.prefixes
	hfst-compose-intersect -1 $< -2 .deps/$(PREFIX2).autobil.prefixes -o $@

$(PREFIX2).automorf.hfst: .deps/$(PREFIX2).automorf-trimmed.hfst
	hfst-fst2fst -w -i $< -o $@

$(PREFIX2).automorf-untrimmed.hfst: .deps/$(LANG2).automorf.hfst
	hfst-fst2fst -w -i $< -o $@

# -------------------
# Inari Saami generation:
# ---------------------

.deps/$(LANG2).autogen.hfst: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).RL.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

$(PREFIX1).autogen.hfst: .deps/$(LANG2).autogen.hfst
	hfst-fst2fst -O -i $< -o $@


###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).mor.rlx.bin: $(AP_SRC1)/$(LANG1).mor.rlx.bin gt2apertium.cg3r
	cg-relabel $^ $@

$(PREFIX1).syn.rlx.bin: $(AP_SRC1)/$(LANG1).syn.rlx.bin gt2apertium.cg3r
	cg-relabel $^ $@


$(PREFIX2).mor.rlx.bin: $(AP_SRC2)/$(LANG2).mor.rlx.bin gt2apertium.cg3r
	cg-relabel $^ $@

$(PREFIX2).syn.rlx.bin: $(AP_SRC2)/$(LANG2).syn.rlx.bin gt2apertium.cg3r
	cg-relabel $^ $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1).autolex.bin: $(BASENAME).$(PREFIX1).lrx
	lrx-comp $< $@

$(PREFIX2).autolex.bin: $(BASENAME).$(PREFIX2).lrx
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_sme_smndir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_sme_smn_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t3x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "ja" | apertium -d . sme-smn | tee .test-mt
	@echo "já" > .test-ref
	@diff .test-ref .test-mt
	echo "já" | apertium -d . smn-sme | tee .test-mt
	@echo "ja" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt

