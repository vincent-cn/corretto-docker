FROM alpine:latest

ARG version=11.0.7.10.1

RUN wget -O /etc/apk/keys/amazoncorretto.rsa.pub https://apk.corretto.aws/amazoncorretto.rsa.pub && \
    echo "https://apk.corretto.aws" >> /etc/apk/repositories && \
    apk add --no-cache amazon-corretto-11=$version-r0 && \
    JAVA_HOME=/usr/lib/jvm/default-jvm && \
    PATH=$PATH:$JAVA_HOME/bin && \
    jlink --endian little --release-info $JAVA_HOME/release \ 
        --add-modules "java.base,java.datatransfer,java.desktop,java.instrument,java.logging,java.management,java.management.rmi,java.naming,java.prefs,\
java.rmi,java.security.sasl,java.xml,jdk.internal.vm.ci,jdk.jfr,jdk.management,jdk.management.jfr,jdk.management.agent,jdk.net,jdk.sctp,jdk.unsupported,\
jdk.naming.rmi,java.compiler,jdk.aot,jdk.internal.vm.compiler,jdk.internal.vm.compiler.management,java.se,java.net.http,java.scripting,java.security.jgss,\
java.smartcardio,java.sql,java.sql.rowset,java.transaction.xa,java.xml.crypto,jdk.accessibility,jdk.charsets,jdk.crypto.cryptoki,jdk.crypto.ec,\
jdk.dynalink,jdk.httpserver,jdk.jsobject,jdk.localedata,jdk.naming.dns,jdk.scripting.nashorn,jdk.security.auth,jdk.security.jgss,jdk.xml.dom,jdk.zipfs,\
jdk.jdwp.agent,jdk.pack,jdk.scripting.nashorn.shell,jdk.jcmd,jdk.jfr" \
        --no-man-pages --no-header-files --strip-debug --output /temp/java-11-amazon-corretto


FROM alpine:latest
COPY --from=0 /temp/java-11-amazon-corretto /usr/lib/jvm/java-11-amazon-corretto
ENV LANG C.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/java-11-amazon-corretto
ENV PATH=$PATH:/usr/lib/jvm/java-11-amazon-corretto/bin
