#FROM gcr.io/spiffe-io/spire-agent:1.1.0 as spire
FROM ghcr.io/spiffe/spire-agent:1.9.1 as spire

#FROM envoyproxy/envoy-alpine:v1.20.0
FROM ikubernetes/envoy-alpine:v1.29.2
RUN mkdir -p /opt/spire/conf/agent
RUN mkdir -p /opt/spire/data/agent
COPY --from=spire /opt/spire/bin/spire-agent /opt/spire/bin/spire-agent
COPY conf/envoy.yaml /etc/envoy/envoy.yaml
COPY conf/spire-agent.conf /opt/spire/conf/agent/agent.conf
COPY conf/agent.key.pem /opt/spire/conf/agent/agent.key.pem
COPY conf/agent.crt.pem /opt/spire/conf/agent/agent.crt.pem
COPY web-server /usr/local/bin/web-server

WORKDIR /opt/spire
CMD /usr/local/bin/envoy -l debug -c /etc/envoy/envoy.yaml --log-path /tmp/envoy.log
