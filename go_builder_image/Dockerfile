# Go builder image for Openshift s2i
FROM registry.access.redhat.com/ubi8:8.3

ENV NAME=golang \
    VERSION=1.14 \
    ARCH=x86_64 \
    GOCACHE=/tmp/src \
    APPROOT=/opt/app-root

LABEL maintainer="Tale Toul <tale.toul@gmail.com>"

LABEL io.k8s.description="Builer image for go" \
      io.k8s.display-name="go builder image" \
      io.openshift.expose-services="8080:http" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.tags="builder,go,golang"

RUN yum install -y --disableplugin=subscription-manager --setopt=tsflags=nodocs golang && \
    yum clean all -y --disableplugin=subscription-manager 

COPY ./s2i/bin/ /usr/libexec/s2i

RUN chown -R 1001:0 /usr/libexec/s2i && \
    chmod -R +x /usr/libexec/s2i/. && \
    mkdir -p $APPROOT && \
    chown -R 1001:0 $APPROOT && \
    chmod -R g=u $APPROOT

USER 1001

WORKDIR $APPROOT

EXPOSE 8080

CMD ["/usr/libexec/s2i/usage"]
