
# Build environment can be configured the following
# environment variables:
#   CC : Specify the C compiler to use
#   CFLAGS : Specify compiler options to use

BIN = ringserver

SRCS = stack.c rbtree.c logging.c clients.c slclient.c dlclient.c \
       http.c dsarchive.c mseedscan.c generic.c ring.c ringserver.c
OBJS = $(SRCS:.c=.o)

# Standard compiler parameters
CFLAGS += -D_REENTRANT -D_POSIX_PTHREAD_SEMANTICS -I../libmseed -I../mxml -I../pcre 

LDLIBS  = ../pcre/.libs/libpcre.a ../libmseed/libmseed.a ../mxml/libmxml.a -lpthread

# For SunOS/Solaris uncomment the following line
#LDLIBS = ../pcre/.libs/libpcre.a ../libmseed/libmseed.a ../mxml/libmxml.a -lpthread -lsocket -lnsl -lrt

all: $(BIN)

$(BIN): $(OBJS)
	$(CC) $(CFLAGS) -o ../$(BIN) $(OBJS) $(LDFLAGS) $(LDLIBS)

clean:
	rm -f $(OBJS) ../$(BIN)

install:
	mkdir -p /ringserver
	install -D ../$(BIN) /usr/bin
	install -D ringserver.conf.example /etc/ringserver.conf
	install -D -m 644 ringserver.service /etc/systemd/system
	@echo
	@echo "**************************************************************"
	@echo "*** Run 'sudo make activate' to start ringserver as a systemd service."
	@echo "**************************************************************"

activate:
	systemctl stop ringserver
	systemctl disable ringserver
	systemctl enable ringserver
	systemctl start ringserver
	systemctl status ringserver

deactivate:
	systemctl stop ringserver
	systemctl disable ringserver
	systemctl status ringserver

