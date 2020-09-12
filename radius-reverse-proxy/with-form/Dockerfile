ARG APACHE_VERSION=2.4
FROM httpd:${APACHE_VERSION}-alpine          


RUN apk --update --no-cache add apache-mod-auth-radius

# sudo a2enmod proxy
# sudo a2enmod proxy_http
# sudo a2enmod proxy_balancer
# sudo a2enmod lbmethod_byrequests
RUN sed -i \
        -e 's/^#\(LoadModule .*mod_proxy.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_proxy_http.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_proxy_balancer.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_lbmethod_byrequests.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_slotmem_shm.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_request.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_auth_form.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_session.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_session_cookie.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_session_crypto.so\)/\1/' \
        conf/httpd.conf

RUN echo "LoadModule radius_auth_module /usr/lib/apache2/mod_auth_radius.so" >> conf/httpd.conf

COPY vhost.auth-form.conf /tmp/vhost.conf
# OR /usr/local/apache2/conf/extra/httpd-vhosts.conf
RUN cat /tmp/vhost.conf >> conf/httpd.conf && \
    mkdir -p /usr/local/apache2/htdocs/public

COPY login.html /usr/local/apache2/htdocs/login.html
