FROM oott123/novnc

ENV VNC_GEOMETRY=1280x960 \
    VNC_PASSWD=z5xVncPd \
    USER_PASSWD=user \
    CHROME_DEVEL_SANDBOX=/usr/local/sbin/chrome-devel-sandbox

RUN apt-get update \
    && apt-get -y install software-properties-common apt-transport-https tzdata \
    && curl -sSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
    && echo "deb https://deb.nodesource.com/node_11.x xenial main" | sudo tee /etc/apt/sources.list.d/nodesource.list \
    && echo "deb-src https://deb.nodesource.com/node_11.x xenial main" | sudo tee -a /etc/apt/sources.list.d/nodesource.list \
    && add-apt-repository -y ppa:jtaylor/keepass \
    && apt-get update \
    && apt-get install -y keepass2 nodejs libmono-system-xml-linq4.0-cil libmono-system-data-datasetextensions4.0-cil libmono-system-runtime-serialization4.0-cil mono-mcs unzip libasound2 libnss3

RUN wget https://raw.github.com/pfn/keepasshttp/master/KeePassHttp.plgx \
    && cp KeePassHttp.plgx /usr/lib/keepass2/

COPY ./ /bot/

RUN cd /bot && npm install \
    && sh /bot/install-npm-deps.sh \
    && mv vncmain.sh /app/vncmain.sh \
    && chmod +x /app/vncmain.sh

