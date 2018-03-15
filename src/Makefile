# -*- mode: makefile-gmake; coding: utf-8 -*-

# Copyright (C) 2014, Oscar Acena <oscaracena@gmail.com>
# This software is under the terms of Apache License v2 or later.

TARGETS  = gattlib.so
OBJECTS  = att.o crypto.o uuid.o gatt.o gattrib.o btio.o log.o utils.o \
	   gattservices.o gattlib.o bindings.o beacon.o

PY_SHORT_VERSION = $(shell python -c "import sys; vers = sys.version_info; print(str(vers.major) + str(vers.minor), sep='')")
PYTHON_CONFIG = python-config
BOOST_PYTHON  = boost_python-py$(PY_SHORT_VERSION)

CFLAGS  += -ggdb -fPIC -Wall $$($(PYTHON_CONFIG) --includes) \
	   -Ibluez -Ibluez/lib -Ibluez/btio $$(pkg-config --cflags glib-2.0)

CFLAGS  += -DVERSION='"5.49"'
CXXFLAGS = $(CFLAGS)
LDFLAGS  = -l$(BOOST_PYTHON) -lboost_thread -lbluetooth \
	   $$(pkg-config --libs glib-2.0)

vpath %.c bluez/attrib
vpath %.c bluez/src
vpath %.c bluez/src/shared
vpath %.c bluez/lib
vpath %.c bluez/btio

all: $(TARGETS)

gattlib.so: $(OBJECTS)
	$(CXX) $(CXXFLAGS) -shared -o $@ $^ $(LDFLAGS)

.PHONY: clean
clean:
	rm -f *.o *.so* *~
