# ***************************************************************** #
# This is a makefile that builds the Hungarian morphological parser #
# ***************************************************************** #

XFST = xfst
LEXC = lexc
TWOLC = twolc

ifeq (victorio.uit.no, $(shell hostname))
XFST = /opt/sami/xerox/c-fsm/ix86-linux2.6-gcc3.4/bin/fst -utf8
LEXC = /opt/sami/xerox/bin/lexc -utf8
TWOLC = /opt/sami/xerox/bin/twolc -utf8
endif

scripts=$(GTHOME)/gt/script

LEX = hun-lex.txt #\
#	  pron-hun-lex.txt 
#	  noun-hun-lex.txt \
#	  noun-hun-morph.txt \
#	  propernoun-hun-lex.txt \
#	  propernoun-hun-morph.txt \
#	  adj-hun-lex.txt \
#	  adj-hun-morph.txt \
#	  verb-hun-lex.txt \
#	  verb-hun-morph.txt \
#	  adv-hun-lex.txt \
#	  abbr-hun-lex.txt \
#	  acro-hun-lex.txt \
#	  punct-hun-lex.txt \
#	  numeral-hun-lex.txt \
#	  pp-hun-lex.txt \
#	  cc-hun-lex.txt \
#	  cs-hun-lex.txt \
#	  interj-hun-lex.txt \
#	  det-hun-lex.txt

all: ihun.fst

# The ultimate goal is to build ihun.fst, the generator
# This goal depends on hun.save being up to date.

ihun.fst: ../bin/ihun.fst
../bin/ihun.fst: ../bin/hun.save \
				 ../bin/hun.fst \
				 ../bin/tok.fst \
#				 ../bin/abbr.txt \
            	 ../bin/allcaps.fst #\
#            	 ../bin/hun-dis.bin \
#            	 ../bin/hun-dep.bin 

	@echo
	@echo "*** Building the inverse ihun.fst ***"
	@echo
	@printf "load $< \n\
	invert net \n\
	save stack $@ \n\
	quit \n" > ../tmp/ihun-fst-script
	$(XFST)  < ../tmp/ihun-fst-script
	@rm -f ../tmp/ihun-fst-script


# The first goal is to build hun.fst, the analyzer.
# This goal depends on hun.save and inituppercase.fst being up to date
hun.fst: ../bin/hun.fst
../bin/hun.fst: ../bin/hun.save \
				../bin/inituppercase.fst \
				../bin/allcaps.fst \
				../bin/tok.fst 

	@echo
	@echo "*** Building hun.fst ***" ;
	@echo
	@printf "read regex @\"../bin/hun.save\" \
					.o. @\"../bin/inituppercase.fst\" ; \n\
	save stack $@ \n\
	quit \n" > ../tmp/hun-fst-script
	$(XFST)  < ../tmp/hun-fst-script
	@rm -f ../tmp/hun-fst-script


# Here we make the abbrevation file for our current preprocessor, 
# the perl-based preprocess (located in the script catalogue)
empty:=
comma:=,
space:=$(empty) $(empty)
ABBRSRCS=$(subst $(space),$(comma),$(LEX))

abbr: ../bin/abbr.txt
../bin/abbr.txt: $(scripts)/abbr-extract.pl \
				 $(scripts)/langTools/Util.pm \
				 $(LEX)
	@echo
	@echo "*** Extracting abbreviations from abbr-hun-lex.txt to abbr.txt ***" ;
	@echo
	@perl -I $(scripts) $(scripts)/abbr-extract.pl \
		--output=$@ \
		--abbr_lex=abbr-hun-lex.txt \
		--lex=$(ABBRSRCS)


allcaps.fst: ../bin/allcaps.fst
../bin/allcaps.fst: allcaps.xfst
	@echo
	@echo "*** Building $(notdir $@) ***" ;
	@echo
	$(XFST) -e "source < $< " \
			-e "save stack   $@ " \
			-stop


inituppercase.fst: ../bin/inituppercase.fst
../bin/inituppercase.fst: inituppercase.regex
	@echo
	@echo "*** Building $(notdir $@) ***" ;
	@echo
	$(XFST) -e "read regex < $< " \
			-e "save stack   $@ " \
			-stop


# The third goal is to build hun.save
# This goal depends on twol-hun.bin and a bunch of lexicon files
hun.save: ../bin/hun.save
../bin/hun.save: ../bin/twol-hun.bin $(LEX)
	@echo
	@echo "*** Building hun-lex.save ***" ;
	@echo
	printf "compile-source $(LEX)  \n\
	read-rules $< \n\
	compose-result \n\
	save-result $@ \n\
	quit \n" > ../tmp/hun-lex-save-script
	$(LEXC)  < ../tmp/hun-lex-save-script
	rm -f ../tmp/hun-lex-save-script


# The fourth goal is to build twol-hun.bin
# This goal depends on twol-hun.txt
twol-hun.bin: ../bin/twol-hun.bin
../bin/twol-hun.bin: twol-hun.txt
	@echo
	@echo "*** Building twol-hun.bin ***" ;
	@echo
	@printf "read-grammar twol-hun.txt \n\
	compile \n\
	save-binary ../bin/twol-hun.bin \n\
	quit \n" > ../tmp/twol-hun-script
	$(TWOLC)  < ../tmp/twol-hun-script
	@rm -f ../tmp/twol-hun-script

# Here we include a preprocessor.
# This goal depends on tok.regex
tok.fst: ../bin/tok.fst 
../bin/tok.fst: tok.xfst
	@echo
	@echo "*** Building the tokenizer $(notdir $@) ***" ;
	@echo
	@printf "source $< \n\
	save stack $@ \n\
	quit \n" > ../tmp/tok-script
	$(XFST)  < ../tmp/tok-script
	@rm -f ../tmp/tok-script

### # Let us just make a binary disambiguator
### # and dependency grammar.
### # They can be used instead of the source files.
### dis-bin: ../bin/hun-dis.bin
### ../bin/%.bin: %.rle
### 	@echo
### 	@echo "*** Building a binary $(notdir $@) ***" ;
### 	@echo
### 	@vislcg3 --grammar $< \
### 			 --grammar-only \
### 			 --grammar-bin $@ \
### 			 -C UTF-8

# "make clean" is there to remove the binary files at will.
clean:
	@rm -f ../bin/*
