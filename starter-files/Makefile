ALL_TESTS := $(wildcard tests/*.uc)
PHASE1_TESTS := tests/type_clash_user.uc tests/function_clash_primitive.uc
PHASE2_TESTS := tests/phase2.uc tests/unknown_type.uc
PHASE3_TESTS := tests/unknown_function.uc
PHASE4_TESTS := tests/variable_clash.uc
PHASE5_TESTS := tests/break_not_in_loop.uc
PHASE6_TESTS := $(filter-out $(PHASE1_TESTS) $(PHASE2_TESTS) $(PHASE3_TESTS) $(PHASE4_TESTS) $(PHASE5_TESTS),$(ALL_TESTS))
PYTHON := python3
FLAGS := -S -T

all: test

test: phase1 phase2 phase3 phase4 phase5 phase6

phase1: $(PHASE1_TESTS:.uc=.test)

phase2: $(PHASE2_TESTS:.uc=.test)

phase3: $(PHASE3_TESTS:.uc=.test)

phase4: $(PHASE4_TESTS:.uc=.test)

phase5: $(PHASE5_TESTS:.uc=.test)

phase6: $(PHASE6_TESTS:.uc=.test)

%.test: %.uc
	@echo "Testing $<..."
	$(PYTHON) ucc.py $(FLAGS) $< > $(<:.uc=.out) || true
	$(PYTHON) ucccheck.py $<
	@echo

STYLE_SOURCES := ucbase.py ucexpr.py ucfunctions.py ucstmt.py uctypes.py
PYLINT_FLAGS := --max-args=6 --max-module-lines=1500

style: style-pycode style-pydoc style-pylint

style-pycode:
	pycodestyle $(STYLE_SOURCES)

style-pydoc:
	pydocstyle $(STYLE_SOURCES)

style-pylint:
	pylint $(PYLINT_FLAGS) $(STYLE_SOURCES)

clean:
	rm -f tests/*.out tests/*.types
