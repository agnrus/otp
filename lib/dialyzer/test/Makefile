include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Files
# ----------------------------------------------------

AUXILIARY_FILES=\
	dialyzer.spec\
	dialyzer_test_constants.hrl\
	dialyzer_common.erl\
	file_utils.erl\
	plt_SUITE.erl

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------

RELSYSDIR = $(RELEASE_PATH)/dialyzer_test

# ----------------------------------------------------
# Release Target
# ----------------------------------------------------

include $(ERL_TOP)/make/otp_release_targets.mk

release_tests_spec:
	$(INSTALL_DIR) $(RELSYSDIR)
	chmod -f -R u+w $(RELSYSDIR)
	$(INSTALL_DATA) $(AUXILIARY_FILES) $(RELSYSDIR)
	@tar cf - *_SUITE_data | (cd $(RELSYSDIR); tar xf -)
	cd $(RELSYSDIR);\
	erl -make;\
	erl -noshell -run dialyzer_common create_all_suites -s erlang halt
