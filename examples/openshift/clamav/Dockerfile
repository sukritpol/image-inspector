#FROM openshift/origin:latest
FROM openshift/origin:v3.6.1

# Reset the entrypoint
ENTRYPOINT ["/bin/sh", "-c"]

RUN yum install -y epel-release \
      && yum install -y clamav-server clamav-scanner clamav-data clamav-update --disablerepo=origin-local-release \
      && mkdir -p /image-data && chmod 0777 /image-data \
      && freshclam

# Copy the default clamav configuration. For custom configuration, create a VOLUME.
COPY clamd.conf /etc/clamd.d/local.conf
COPY freshclam.conf /etc/clamd.d/freshclam.conf

# Copy the scanner binary
COPY run-clam-scan/run-clam-scan /usr/bin/run-clam-scan

# Copy the image inspector binary
COPY image-inspector /usr/bin/image-inspector

CMD ["/usr/bin/run-clam-scan"]
