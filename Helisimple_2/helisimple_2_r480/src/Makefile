include Mk/local.Mk
SUBDIRS+=common
SUBDIRS+=gui
SUBDIRS+=control
SUBDIRS+=imageproc
SUBDIRS+=main

OBJS=$(wildcard ../obj/*.o)
LXXLIBS+=-L/usr/local/lib
LXXLIBS+=-lSDL
LXXLIBS+=-lz
LXXLIBS+=-lavcodec
LXXLIBS+=-lswscale
LXXLIBS+=-lpthread
LXXLIBS+=-lavutil

COPY_ETC_CMD=../etc/copy.sh
COPY_ETC_SRC=../etc
COPY_ETC_DST=../bin

heli: all obj
	$(CXX) $(CXXDEFINE) -o ../bin/$@  $(OBJS)  $(CXXFLAGS) $(LXXLIBS) 

export: moveCircleAway clean zip moveCircleBack

zip:	clean
	rm -rf ../../helisimple_2_web
	cp -r ../../helisimple_2/ ../../helisimple_2_web/

moveCircleAway:
	mv imageproc/CCircleDetect.o ../../ 
	mv imageproc/CCircleDetect.cpp ../../
	mv ../../CCircleDetect.o  imageproc/

moveCircleBack:
	mv ../../CCircleDetect.cpp imageproc 

all:
	echo $(OPSYS)
	@for i in $(SUBDIRS) ;\
	do \
	echo "making" all "in $(CURRENT_DIR)/$$i..."; \
	$(MAKE) -C $$i all; \
	done

obj: all
	echo "Copy objs"
	@for i in $(SUBDIRS) ;\
	do \
	echo "coping all in $(CURRENT_DIR)/$$i..."; \
	cp $$i/*.o ../obj; \
	done


etc: ../bin/.etc

	#cp -r ../etc/$$i ../bin; \
	#
../bin/.etc:
	echo "Copy dirs from etc"
	$(COPY_ETC_CMD) $(COPY_ETC_SRC) $(COPY_ETC_DST)
	touch ../bin/.etc

cleanetc:
	rm -f ../bin/.etc	

	#cp -r ../etc/$$i ../bin; 
forceetc:
	echo "Copy dirs from etc"
	$(COPY_ETC_CMD) $(COPY_ETC_SRC) $(COPY_ETC_DST)
	touch ../bin/.etc

clean:
	echo $(OPSYS)
	@for i in $(SUBDIRS) ;\
	do \
	echo "cleaning" all "in $(CURRENT_DIR)/$$i..."; \
	$(MAKE) -C $$i clean; \
	done
	echo "cleaning all objs"
	rm -f ../obj/*.o
	echo "cleaning binaries"
	rm -f ../bin/*
