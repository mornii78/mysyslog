CC = gcc
CFLAGS = -Wall -Werror -I../libmysyslog/include
LDFLAGS = -L../libmysyslog -L../libmysyslog-text -L../libmysyslog-json
LDLIBS = /home/astra/Desktop/mysyslog/libmysyslog/libmysyslog.a /home/astra/Desktop/mysyslog/libmysyslog-text/libmysyslog-text.a /home/astra/Desktop/mysyslog/libmysyslog-json/libmysyslog-json.a
TARGET = mysyslog-daemon
SRC = src/mysyslog-daemon.c
OBJ = $(SRC:.c=.o)
DEB_DIR = mysyslog-daemon_deb

CONFIG_FILE = /home/astra/Desktop/mysyslog/config/mysyslog.cfg

all: $(TARGET)

$(TARGET): $(OBJ)
	$(CC) -o $@ $^ $(LDFLAGS) $(LDLIBS)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) $(TARGET)
	rm -f *.deb
	rm -r $(DEB_DIR)

deb: all
	mkdir -p $(DEB_DIR)/DEBIAN $(DEB_DIR)/usr/bin $(DEB_DIR)/etc/mysyslog
	echo "Package: libmysyslog-daemon" > $(DEB_DIR)/DEBIAN/control
	echo "Version: 1.0" >> $(DEB_DIR)/DEBIAN/control
	echo "Section: admin" >> $(DEB_DIR)/DEBIAN/control
	echo "Priority: optional" >> $(DEB_DIR)/DEBIAN/control
	echo "Architecture: amd64" >> $(DEB_DIR)/DEBIAN/control
	echo "Maintainer: AACnotAliVe <mrlenorgenri@gmail.com>" >> $(DEB_DIR)/DEBIAN/control
	echo "Depends: libmysyslog" >> $(DEB_DIR)/DEBIAN/control
	echo "Description: A daemon for the mysyslog" >> $(DEB_DIR)/DEBIAN/control
	cp $(TARGET) $(DEB_DIR)/usr/bin/
	cp $(CONFIG_FILE) $(DEB_DIR)/etc/mysyslog/
	dpkg-deb --build $(DEB_DIR)
	mv mysyslog-daemon_deb.deb mysyslog-daemon_1.0_amd64.deb

