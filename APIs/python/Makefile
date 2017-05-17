
# You may need to change these paths to match your installation.
# Alternatively, you can call 'make' overriding variable values, E.g.:
#     make FREELINGDIR=/my/freeling/dir PYTHONDIR=/my/python/dir

FREELINGDIR = /usr/local
PYTHONVER = python3.4
PYTHONDIR = /usr/include/$(PYTHONVER)

# OSX Users should be aware of headers location and also lib location, since OSX does not put python library in /usr/local
# Depending on your Python installation, Python lib would be at one of the sugested places:
# /usr/local/Cellar/python3/$(PYTHONVER)/Frameworks/Python.framework/Versions/$(PYTHONVER)/lib
# /Library/Frameworks/Python.framework/Versions/$(PYTHONVER)/lib

# A suggested configuration for OSX would be
# PYTHONVER=python3.6m
# PYTHONDIR=/usr/local/Cellar/python3/3.6.1/Frameworks/Python.framework/Versions/3.6

# And be sure to comment line 22 and uncomment line 24

_freeling.so: freeling_pythonAPI.cxx
	g++ -shared -o _freeling.so freeling_pythonAPI.cxx -lfreeling -I$(FREELINGDIR)/include -L$(FREELINGDIR)/lib -I$(PYTHONDIR) -fPIC -std=gnu++0x
#       Mac OSX users:  Comment the line above, and uncomment the line below:
#	g++ -dynamiclib -o _freeling.so freeling_pythonAPI.cxx -lboost_system -l$(PYTHONVER) -lfreeling -I$(FREELINGDIR)/include -L$(FREELINGDIR)/lib -I$(PYTHONDIR)/include/$(PYTHONVER) -L$(PYTHONDIR)/lib $(CPPFLAGS) $(LDFLAGS) -fPIC  -std=c++0x -v

freeling_pythonAPI.cxx: freeling_pythonAPI.i ../common/freeling.i ../common/templates.i
	swig -python -py3 -c++ -o freeling_pythonAPI.cxx freeling_pythonAPI.i
#       Python2 users: Remove option "-py3" from the above line

clean:
	rm -rf __pycache__ freeling_pythonAPI.cxx _freeling.so freeling.py*
