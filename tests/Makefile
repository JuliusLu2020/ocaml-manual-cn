TOPDIR=$(abspath ../ocaml)
include $(TOPDIR)/Makefile.tools
MANUAL=$(TOPDIR)/../manual

.PHONY: all
all: check-cross-references check-stdlib

.PHONY: tools
tools: cross-reference-checker

cross-reference-checker: cross_reference_checker.ml
	$(OCAMLC) $(TOPDIR)/compilerlibs/ocamlcommon.cma \
	  -I $(TOPDIR)/parsing -I $(TOPDIR)/driver \
	  $< -o $@

.PHONY: check-cross-references
check-cross-references: cross-reference-checker
	$(SET_LD_PATH) \
	  $(OCAMLRUN) ./cross-reference-checker \
	  -auxfile $(MANUAL)/texstuff/manual.aux \
	  $(TOPDIR)/utils/warnings.ml \
	  $(TOPDIR)/driver/main_args.ml \
	  $(TOPDIR)/bytecomp/translmod.ml

.PHONY: check-stdlib
check-stdlib:
	./check-stdlib-modules $(TOPDIR)


.PHONY: clean
clean:
	rm -f *.cm? *.cmx? cross-reference-checker
