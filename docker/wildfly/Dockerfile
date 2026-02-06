FROM quay.io/wildfly/wildfly:latest

USER root
RUN microdnf install -y curl && microdnf clean all
USER jboss

ARG WAR_URL="https://get.jenkins.io/war-stable/latest/jenkins.war"
ARG WAR_NAME="jenkins.war"

ENV APP_LOGS_ROOT_DIR="/opt/jboss/wildfly/custom-logs" \
    APP_LOG_MODE="info"

RUN mkdir -p "${APP_LOGS_ROOT_DIR}" \
    && curl -fsSL "${WAR_URL}" -o "/opt/jboss/wildfly/standalone/deployments/${WAR_NAME}"

EXPOSE 8080 9990

HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=5 \
  CMD curl -fsS http://127.0.0.1:8080/ || exit 1

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
