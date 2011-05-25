NGinx Ubuntu Init Script
========================

Installing Nginx from source on Ubuntu 10.04...


    ## Basic stuff
    apt-get update
    apt-get install build-essential git-core wget

    ## Install PCRE for rewriting
    apt-get install libpcre3 libpcre3-dev

    ## Install ssl
    apt-get install openssl libssl-dev

    ## Download nginx sources
    cd /usr/local/src/
    svn checkout svn://svn.nginx.org/nginx/trunk nginx
    cd nginx/

    ## Configure
    ./configure \
        --prefix="/usr/local" \
        --conf-path="/usr/local/etc/nginx/nginx.conf" \
        --with-http_ssl_module \
        --with-cc-opt="-I /usr/include/" \
        --with-cc-opt="-I /usr/include/openssl/"

    ## Build and install
    make
    sudo make install

    ## Install init script
    cd /usr/local/src/
    git clone git://github.com/brendoncrawford/nginx-init-ubuntu.git
    chmod +x nginx-init-ubuntu/nginx
    mkdir -p /usr/local/etc/init.d/
    cp nginx-init-ubuntu/nginx /usr/local/etc/init.d/nginx
    ln -s /usr/local/etc/init.d/nginx /etc/init.d/nginx
    /usr/sbin/update-rc.d -f nginx defaults

    ## Cleanup stuff</strong>
    rm -f /usr/local/etc/nginx/*.default

