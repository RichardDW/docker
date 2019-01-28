FROM httpd:2.4

RUN	apt-get update && apt-get -y install \
	libapache2-mod-perl2 \
	libarchive-zip-perl \
	libcgi-session-perl

COPY	./primer3plus/ /usr/local/apache2/primer3plus/
COPY	./httpd.conf /usr/local/apache2/conf/httpd.conf

RUN	cd /usr/local/apache2 && chgrp -R www-data primer3plus && \
	mv cgi-bin/ cgi-bin.old && ln -s ./primer3plus/cgi-bin cgi-bin && \
	cp -p /usr/lib/apache2/modules/mod_perl.so /usr/local/apache2/modules && \
	cd /usr/local/apache2/modules && \
	chmod a+x mod_perl.so && \
	chgrp www-data mod_perl.so && \
	cd /usr/local/lib && \
	ln -s /usr/local/apache2/cgi-bin/ site_perl	


